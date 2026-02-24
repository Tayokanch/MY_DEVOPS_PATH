# Object Storage in AWS

`Amazon S3`
- This is an object storage used for storing / uploading files e.g `Image`, `Videos`,` Static web files` , `logs` etc
- This doesnt have a folder strcure
- It can be used to mount or boots


## Storage Classes in S3

`S3 Standard (default)`
- It is the most expensive
- It Data is Available on multiple AZ i.e if One AZ goes down the other one will be avialable 
- It has High 
- It charges based on the amount of Gigabyte we've used per Month
- It also charges egress fee i.e the amount of data we send out will be charged by Gigabyte outbound
- It can be used for Web Applications or anything that needs pur data accessed Immediately.


`S3 Standard-IA(Infrequent Access)`

- This could be used as an alternative for **S3 standard** if our data doesnt need to be access frequently 
- It stores Data in Multiple AZ
- It has a retrieval Fee i.e egress fee 
- Minimum duration charge of 90days
- Minimun size charge of 128 per object


`S3 One Zone-IA`
- This is similar to **S3 Standard-IA** the difference there here is that Data are stored in a Single AZ
- So its cheaper but also charge for egress fee
- Minimum duration charge of 90days
- minimum size charge of 128 kb per Object


`S3 Glacier-Instant`
- This is use for rarely accessed Data, it has the performance of **S3 Standard**
- Minimum duration charge of 90days
- It has a very cheap Cost but **Higher Egress Charges**
- Data Stored are highly Available 
- Cheaper than **S3 standard and S3 AI**


`S3 Glacier-Flexible`
- This is also a Cheaper storage but Data saved here are not readily available. Not ideal for Web Application
- It has a egress charges
- Minimum duration charge of 90days
- minimum size charge of 40 kb per Object
  

`S3 Glacier Deep Archieve`
- This is used to store Data that are almost never needed 
- File are not readily available


`S3 Intelligent-Tiering`

- This automatically reduces storage costs by intelligently moving data to the most cost-effective access tier