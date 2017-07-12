+++
description = "How to use the Environmental Data Commons ID Service"
title = "Signpost ID Service"
date = "2017-07-10T16:43:08+01:00"
draft = false
weight = 200
bref= "What is Signpost and how do I use it?"
toc = true
+++

### Signpost ID Service


The Signpost digital ID system balances the needs of both data archiving for persistent storage, that is, assigning identifiers to unique pieces of information, and also active computation, that is, for finding locations of data on a living system where data may be physically moved or updated. We have constructed a simple implementation of this design in a two-layer identification scheme service with a REST-like API interface.

The top layer utilizes user-defined identifiers. These are flexible, may be of any format, including Archival Resource Keys (ARKs) and Digital Object Identifiers (DOIs), and provide a layer of human readability.  The user-defined identifiers map to hashes of the identified data objects. This additionally allows for mutability by assigning different hashes and allows for reproducibility considerations.

The bottom layer utilizes hash-based identifiers. These are inflexible and identify data objects as unambiguously as possible. Hash-based identifiers guarantee immutability of identified data, allow for identification of duplicated data via hash collisions, and allow for verification upon retrieval. These map to known locations of the identified data.

By utilizing the Signpost digital identifier service, we can relocate data files from our data commons to another commons and no researcher needs to change their code.


### Working with the ID Service

After a user has received their Digital IDs, they may want to confirm integrity and download the data from their query.   Below are some example python functions from the Nexrad [Jupyter example](../python/) that review a txt file from a signpost query, check file integrity, check for a preferred repo, then download the data to the defined in the download_from_arks function.  

```    
   import requests
   import urllib
   import json
   import hashlib
   import os

   #get data from txt file generated from search service
   with open('testarks.txt', 'r') as f:
       file_lines = f.readlines()
             for line in file_lines:
           print line.strip() 
             id_service_arks = [line.strip().decode('utf-8-sig') for line in file_lines]


         # hash provided in signpost should match locally calculated hash
   def confirm_hash(hash_algo, file_,actual_hash):
       with open(file_) as f:
                 computed_hash = hash_algo(f.read()).hexdigest()
 
       if computed_hash == actual_hash:
           return True
       else:
                 return False
    
         def download_from_arks(id_service_arks, intended_dir, hash_confirmation = True, pref_repo='https://griffin-objstore.opensciencedatacloud.org/'):
       hash_algo_dict = {'md5':hashlib.md5, 'sha1':hashlib.sha1, 'sha256':hashlib.sha256}

       for ark_id in id_service_arks:
           signpost_url = 'https://signpost.opensciencedatacloud.org/alias/' + ark_id
     resp = requests.get(signpost_url)         
        
       # make JSON response into dictionary
             signpost_dict = resp.json() #json.load(resp)
             # get repository URLs
             repo_urls = signpost_dict['urls']
             for url in repo_urls:
           print 'url = ', url
     # if preferred repo exists, will opt for that URL
     if pref_repo in url:
                     break
                 # otherwise, will use last url provided

       # if you're not in Jupyter, you can use the requests library to create the files
             r = requests.get(url)
             # need file path for hash validation
             file_name = url.split('/')[-1]
             file_path = os.path.join(intended_dir, file_name)
             f = open(file_path, 'wb')
             f.write(r.content)
             f.close()
        
             # otherwise, we can run this bash command from Jupyter!
             #!sudo wget -P $intended_dir $url
       
             if hash_confirmation:
                 # get dict of hash type: hash
     hashes = signpost_dict['hashes']
     # iterate though list of (hash type, hash) tuples
     for hash_tup in hashes.items():
                     # get proper hash algorithm function
                     hash_algo = hash_algo_dict[hash_tup[0]]
         # fail if not the downloaded file has diff. hash
                     assert confirm_hash(hash_algo, file_path, hash_tup[1]), '%s hash calculated does not match hash in metadata'

         #to download, run function, make sure and have dir 'mayfly_data' created
   download_from_arks(id_service_arks, 'mayfly_data')

```


ARK Key Service
------------------------

The OSDC Public Data Commons features a key service utilizing ARK codes as permanent identifiers to each dataset.  More information can be found here: [https://www.opensciencedatacloud.org/keyservice/](https://www.opensciencedatacloud.org/keyservice/)