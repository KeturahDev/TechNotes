# About

Keturah Smith, May 15 2024

References:
[Official Docs](https://pocketbase.io/docs/), [quick about vid](https://www.youtube.com/watch?v=Wqy3PBEglXQ), [vid about project integration and deployment](https://www.youtube.com/watch?v=gUYBFDPZ5qk&t=56s).

## _Description_:

A backend service.
"A lightweight supabase alternative. which is also an open-source firebase alternative."

## Core Concepts:

- uses SQLite
- scales vertically
- self hostable
- simple to deploy (converts to a single exe)
- Can extend the backend code directly with Go
- Provides
  - user authentication
  - file storage
  - realtime database

## How to Self Host

1. Have a server to host pocketbase (can use linode)
   - register
   - choose region and size for machine
   - note IP address
2. Deploy pocketbase to it
   - download and unzip from official docs
   - To run pocketbase locally
     - at root of project run `./pocketbase serve`
   - To run pocketbase on linode server
     - in terminal run ssh@YOUR_IP: `ssh root@45.xx.xx.xxx`
     - enter password
     - make a remote pocketbase directory: `mkdir pb`
     - upload exe:
       - in project terminal, use secure copy -> `scp pocketbase root@45.xx.xx.xxx:root/pb` copies the local file over to the remote directory
       - when ^ done, go to terminal on linode machine and run `root/pb/pocketbase serve --http="YOUR_IP:80"` http flag makes it available over the internet
3. Modeling Data:
   - access gui with \_url
   - users collection already exists
   - to create a one to many relationship for user
     - creeate new collection
     - add a datatype of Relation called user
     - under the hood, pocketbase creates a foreign key for the user ID on the messages table in SQLite database

**_Production ready steps:_**

- bring domain name to linode
  - automatically gnereates an SSL certificate to serve backend over https
  - has fully featured DNS manager
- mount volume to pb-data directory - allows for adding more GBs for scale
- Set up SystemD Service: automatically restarts pocketbase whenever server reboots

tutorials:

- [Deploy PocketBase on Railway
  ](https://www.shrey.com/blog/deploy-pocketbase-on-railway)

### Projects Used:

- []()
