# Description
Virtual hosting is a method for hosting multiple domain names (with separate handling of each name) on a single server. So, It's make easy to run any project by host name. **Let's create virtual host step by step**.
![image](https://vexxhost.com/wp-content/uploads/2014/02/How-To-Set-Up-Nginx-Virtual-Hosts-on-Ubuntu.png)
## Step 1
 Open your terminal. Keyboard shortcut
 ```
 ctrl + alt + t
 ```
 ## Step 2
 Go to sites-available folder by command
 ```
 cd /etc/nginx/sites-available
 ```
 ## Step 3
 Give read and write permission
 ```
 sudo chmod 777 -R /etc/nginx/sites-available
 ```
 ## Step 4 
 Duplicate deafault file. Make sure you enter your file name whatever you want instead of `your_file_name`.
 ```
 sudo cp /etc/nginx/sites-available/default  /etc/nginx/sites-available/your_file_name.conf
 ```
 ## Step 5
 Open your file with nano editor. Write your file name instead of `your_file_name`
 ```
  sudo nano /etc/nginx/sites-available/your_file_name.conf
 ```
 ## Step 6
Now need to delete all code of this file. So, First cursor at the beginning of a file. Then press below key
 ```
 ctrl + 6
 alt + t
```
It's delete all code of your file.
## Step 7
Then copy below code press `ctrl + c` and paste this code in your terminal press `ctrl + shift + v`
```
server {
        listen   80; 

        root /var/www/html/your_project_name/public;
        index index.html index.htm index.php;

        server_name your_host_name.your_preference    www.your_host_name.your_preference; 
        #example : server_name foobar.com  www.foobar.com



        location / {
                try_files $uri $uri/ /index.php?$query_string;
 		    autoindex on;
  		  autoindex_exact_size off;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/run/php/php7.2-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }
    }

```
Give your project folder name instead of `your_folder_name` in line 42.

Now, write your host name instead of `your_host_name` and write your preference instead of `your_preference` in line 45 like line no 46. Then, save your file press below key 
```
ctrl + x

y

Enter
```
## Step 7 
Now, we need enabled this file. Write below command and make sure you enter your file name istead of `your_file_name`
```
sudo ln -s /etc/nginx/sites-available/your_file_name.conf /etc/nginx/sites-enabled 
```
## Step 8
Now, Go to host file.
```
sudo nano /etc/hosts
```
## Step 9
paste this code top of this line `The following lines are desirable for IPv6 capable hosts`
```
127.0.0.1       www.your_host_name.your_preference    
```
Make sure , you enter your host name and your_preference which you give step 7.
## Step 10
Now, go to browser and write your url like
```
http://www.foobar.com
```
## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.
