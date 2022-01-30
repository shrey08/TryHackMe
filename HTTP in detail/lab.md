### GET request to /room
> GET /room HTTP/1.1  
> Host: tryhackme.com  
> User-Agent: Mozilla/5.0 Firefox/87.0
#### Response
> HTTP/1.1 200 Ok  
> Server: nginx/1.15.8  
> Sat, 29 Jan 2022 23:30:24 GMT  
> Content-Type: text/html; charset=utf-8  
> Content-Length: 233  
> Last-Modified: Sat, 29 Jan 2022 23:30:24 GMT    
> <html>  
> <head>  
> <title>TryHackMe</title>  
> </head>  
> <body>  
> Welcome to the Room page THM{YOU'RE_IN_THE_ROOM}  
> </body>  
> </html>  
### GET request to /blog and id parameter to 1 in the URL field
> GET /blog?id=1 HTTP/1.1  
> Host: tryhackme.com  
> User-Agent: Mozilla/5.0 Firefox/87.0  
#### Response
> HTTP/1.1 200 Ok  
> Server: nginx/1.15.8  
> Sun, 30 Jan 2022 23:14:18 GMT  
> Content-Type: text/html; charset=utf-8  
> Content-Length: 231  
> Last-Modified: Sun, 30 Jan 2022 23:14:18 GMT  
> <html>  
> <head>  
> <title>TryHackMe</title>  
> </head>  
> <body>  
> Viewing Blog article 1 THM{YOU_FOUND_THE_BLOG}  
> </body>  
> </html>  
### DELETE request to /user/1
> DELETE /user/1 HTTP/1.1  
> Host: tryhackme.com  
> User-Agent: Mozilla/5.0 Firefox/87.0  
> Content-Length: 0  
#### Response
> HTTP/1.1 200 Ok  
> Server: nginx/1.15.8  
> Sun, 30 Jan 2022 23:18:49 GMT  
> Content-Type: text/html; charset=utf-8  
> Content-Length: 231  
> Last-Modified: Sun, 30 Jan 2022 23:18:49 GMT  
> <html>  
> <head>  
> <title>TryHackMe</title>  
> </head>  
> <body>  
> The user has been deleted THM{USER_IS_DELETED}  
> </body>  
> </html>  
