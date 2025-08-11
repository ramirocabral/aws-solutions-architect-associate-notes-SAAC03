![[Pasted image 20221031103135.png]]

- Move large amount of data to and from:
  - On-premises/other cloud to AWS (NFS, SMB, HDGS, S3 API) -- **needs agent**.
  - AWS to AWS (different services) -- no agent needed.
- Can synchronize to:
  - [[S3]].
  - [[EFS]].
  - [[FSx]].
- Replication tasks can be scheduler hourly, daily, weekly.
- **IMPORTANT: File permisions and metadata are preserved**.
