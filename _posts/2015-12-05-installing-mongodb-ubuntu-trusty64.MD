---
layout: post
title:  "Installing MongoDB on Ubuntu Linux 14.04 (Trusty)"
date:   2015-12-05 09:00:00 -02:00
categories: software engineering
comments: true
published: true
---
MongoDB is an open source, document-oriented database designed with both scalability and developer agility in mind. Instead of storing your data in tables and rows as you would with a relational database, in MongoDB you store JSON-like documents with dynamic schemas.  <br />
<br />
You can watch this video below for more information:   <br />  
<iframe width="420" height="315" src="https://www.youtube.com/embed/CvIr-2lMLsk" frameborder="0" allowfullscreen></iframe>
<br />  
Basically MongoDB is a non-relational datastore for JSON documents. The documents are stored in a **collection**.
A record in MongoDB is a document, which is a data structure composed of field and value pairs. MongoDB documents are similar to JSON objects. There are some characteristics like:

* schemaless - MongoDB has a dynamic schema which means that 2 (two) documents for example, doesn't need to have the same schema.

* don't support **JOINS**

* don't have **TRANSACTIONS** across multiple documents/collections like a relational database.

and so on...  
<br />
Now that I've introduced you to MongoDB I will show you how to install it on a Linux box.
<br />  
First thing you have to do of course is to download the latest stable version of MongoDB:  

```
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1404-3.0.7.tgz
```  
<br />
Extract the files from the archive you just downloaded:

```  
tar -zxvf mongodb-linux-x86_64-ubuntu1410-clang-3.0.7.tgz
```  

Copy the extracted archive to the target directory which means the location from which MongoDB will run:  
In my case I just renamed the mongodb-linux-x86_64-ubuntu1410-clang-3.0.7 directory to **/mongodb**.

```
mv mongodb-linux-x86_64-ubuntu1404-3.0.7 mongodb
```  
add the following line to your shell’s rc file (e.g. ~/.bashrc):

```
vim ~/.bashrc
export PATH=mongodb-install-directory/bin:$PATH
```  
Replace **mongodb-install-directory** with the path to the extracted MongoDB archive.  
<br />
In my case it was:

```
export PATH=/home/vagrant/mongodb/bin/:$PATH
```

Reload you bashrc configuration by typing the command:

```
source ~/.bashrc
```

Before you start MongoDB for the first time, you have to create the directory in which the **mongod** process will write data. By default, the **mongod** process uses the **/data/db** directory. If you create a directory other than this one, you must specify that directory in the **dbpath** option when starting the **mongod** process.
<br />  
I just created the default directory suggested by MongoDB:

```
sudo mkdir -p /data/db
```

And then I changed the ownership from **root** to my username...

```
sudo chown vagrant:vagrant -R /data
```

...because you have to ensure that the user account running **mongod** has read and write permissions for the directory.  
<br />
Now run the **mongod** process:

```
mongod
```

If you see this line above in your shell...

```
NETWORK  [initandlisten] waiting for connections on port 27017
```

...Congratulations!!! You have just installed MongoDB on Ubuntu Linux 14.04.  
<br />
See you next time.  
<br />
Source: MongoDB official website - [Installing MongoDB on Linux](https://docs.mongodb.org/master/tutorial/install-mongodb-on-linux/)
