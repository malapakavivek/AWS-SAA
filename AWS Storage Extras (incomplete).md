- - - 
### AWS Snow Family 

- Portable devices 
- collect and process data at the edge locations 
- migrate data in and out of AWS

- Snowcone - migration size up to terabytes
- Snowball Edge - migration size up to petabytes

if you have 
- limited connectivity 
- limited bandwidth
- high network costs

use AWS snow family - (offline devices which perform data migration)

Note: if it takes more than a week to upload data through a network, use snowball devices! 

![[Pasted image 20240918103503.png|400]]

use cases: preprocess data, machine learning and media

- Snowball cannot import into glacier directly 

- snowball -----> amazon s3 -------> amazon glacier
       (import)        (lifecycle policy)

---

### Amazon FSx 

- launch 3rd party high performance file systems on AWS

![[Pasted image 20240918150121.png|300]]

###### Amazon FSx for Windows
