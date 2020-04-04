

1.  Configure  [`origin`](https://help.github.com/en/articles/configuring-a-remote-for-a-fork)  in your project. From your site’s root directory, set the URL for  `origin`  to your new repo (otherwise you’ll be trying to push changes to  `google/docsy`  rather than to your repo):
    
    ```
    git remote set-url origin https://github.com/MY-SITE/EXAMPLE.git
    
    ```
    
2.  Verify that your remote is configured correctly by running:
    
    ```
    git remote -v
    
    ```
    
3.  Push your Docsy site to your repository:
    
    ```
    git push -u origin master
    ```
> [Source : ](https://).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MTM1NDMwODRdfQ==
-->