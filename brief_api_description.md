# Brief API description

| URL                             | Method | Description                |
| :------------------------------ | ------ | ----------------------------- |
| /register                       | POST   | Register<br />POST /register<br />{<br/>&nbsp;&nbsp;&nbsp;&nbsp;'id': 'user_id',<br />    'nickname': 'nickname'(optional)<br />} |
| /login | POST | Login<br />POST /login<br />{<br />    "username": "username",<br />    "password": "some password"<br />}<br />Status code 200 for success<br />{<br />    "login": "success",<br />    "token": "jwt的token",<br />    "ipfs": "user的ipfs id"<br />} |
| /avatar | POST | Setting avatar<br />POST /avatar<br />{<br/>    'avatar_ipfs': 'ipfs to the avatar image'<br />} |
| /avatar/<user_id> | GET | Get avatar by user_id<br />GET /avatar/user_id |
| /nickname                       | POST   | Set nickname<br />POST /nickname<br />{<br/>    'nickname': 'nickname'<br />} |
| /nickname/<user_id>             | GET    | Get nickname by user_id<br />GET /nickname/user_id |
| /backimg | POST | Setting background image of user<br />POST /backimg<br />{<br />    "backimg_ipfs": "ipfs address of background image"<br />} |
| /backimg/<user_id> | GET | Get background image of user |
| /user-sig | POST | Set user signature<br />POST /user-sig<br />{<br/>    'sig': 'new signature'<br />} |
| /user-sig/<user_id> | GET | Get signature by user_id<br />GET /user-sig/user_id |
| /user/<user_id>?page=2 | GET | Get user timeline by user_id |
| /rss | GET | Get a list of recommended rss |
| /ruser | GET | Get a list of recommended users                              |
| /user-status/<user_id> | GET | Check if user_id is already followed                         |
| /rss-status | GET | Check if the url has been subscribed<br />{''url":"https://www.solidot.org/index.rss"} |
| /subscription                   | POST | Add a subscription<br />POST /subscription<br />{<br/>    'url': 'https://www.solidot.org/index.rss',<br />    'is_user': 'no',<br />    'category_id': u'category id'(optional)<br />} |
| /subscription                   | GET    | View the content of a feed<br />GET /subscription<br />{<br/>    'url': 'https://www.solidot.org/index.rss',<br />    'is_user': 'no',<br />    'page': 1<br />} |
| /subscription                   | DELETE | Delete subscription<br />DELETE /subscription<br />{<br/>    'url': 'https://www.solidot.org/index.rss',<br />    'is_user': 'no',<br />} |
| /category                       | POST   | Create new category<br />POST /category<br />{<br/>    'category_name': 'IT news'<br />} |
| /category                       | PUT    | Modify category name<br />PUT /category<br />{<br/>    'category_id': 'category_id'<br />    'category_name': 'IT News'<br />} |
| /category | GET | Get all categories |
| /category-posts/<category_id>   | GET    | Get the list of posts under category_id |
| /category-sources/<category_id> | GET    | Get the list of subscriptions under category_id<br />GET /category-sources/category_id |
| /file-meta | POST | Upload file metadata information, called before uploading the file<br />{<br />    "filename":"filename",<br />    "filetype": "file type by extension"<br />}<br />Status code 200:<br />{<br />    "upload_url": "The upload post address of the file to be uploaded"<br />}<br />POST the file to the url then the file will be uploaded. |
| /file/<hex_id>             | POST   | Upload the file, the file binary content directly in the post's data, hex_id needs to be obtained after the /file-meta post file metadata.<br />Status code: 201 success<br />{<br />    "ipfs": "the ipfs id of the uploaded file"<br />} |
| /post                           | POST   | User create new post<br />POST /post<br />{<br/>    'title': 'test title',<br />    'description': 'test content',<br />    'images': [ipfs1, ipfs2, ipfs3, ...], <br />    'files': [ipfs1, ipfs2, ipfs3, …],<br />    'url': 'http://solidot.org',<br />    'board': 'board name'<br />} |
| /post                           | GET    | GET post by ipfs id<br />GET /post<br />{<br />    'ipfs': 'ipfs id'<br />} |
| /post                           | DELETE | Delet post by ipfs id<br />DELETE /post<br />{<br />    'ipfs': 'ipfs id'<br />} |
| /comments/<ipfs_hash>           | GET    | Get comments of post by ipfs<br />GET /comments/<ipfs_hash>?page=1 |
| /comments/<ipfs_hash>           | POST   | Add a comment<br />POST /comments/<ipfs_hash><br />{<br />    'content': 'Comment content'<br />}<br />Status code 201 for success |
| /comments/<ipfs_hash>           | DELETE | Delete a comment |
| /like/<ipfs_hash>               | POST   | Like a post<br />POST /like/<ipfs_hash><br />Status code 201 for success |
| /like/<ipfs_hash>               | DELETE | Unlike a post<br />DELETE /like/<ipfs_hash><br />Status code 204 for success |
| /dislike/<ipfs_hash> | POST | Dislike a post<br />POST /dislike/<ipfs_hash><br />Status code 201 for success |
| /dislike/<ipfs_hash> | DELETE | Undislike a post<br />DELETE /dislike/<ipfs_hash><br />Status code 204 for success |
| /msg/<user_id>                  | POST   | Send a private message to another user by user_id<br />POST /msg/<user_ipfs_id><br />{<br />    "msg": "PM content"<br />} |
| /msg/<user_id>                  | GET    | GET /msg/<user_ipfs_id><br />{<br />    "start": "paging parameter, get lastest 100 msg from start number"<br />}<br />If len(return list) is less than 100, means there are no more msgs. |
| /notification | GET | GET /notification<br />Get notifications:<br />{<br />    'follow': [list of new followers], <br />    'comment': [list of new comments],<br />    'like': [list of been liked posts]<br />} |
| /notification-count | GET | GET /notification-count<br />Get notification count |
| /myboards | GET | GET /myboards<br />Get the boards list that the user created |
| /board-hot | GET | GET /board-hot<br />The hot board list |
| /board-search | GET | GET /board-search<br />Search board:<br />{<br />    'keywords': 'search keywords' <br />} |
| /board | GET | GET /board<br />Get list of posts by boardname:<br />{<br />    'boardname': board, <br />    'start': start paging,<br />} |
| /board | POST | POST /board<br />Create board:<br />{<br />    'boardname': name of board, <br />    'description': board description,<br />    'avatar_ipfs': board avatar ipfs<br />} |
| /board-info | GET | GET /board-info<br />Get board information:<br />{<br />    'boardname': board name, <br />} |
| /follow-board | POST | POST /follow-board<br />Follow board:<br />{<br />    'boardname': boardname, <br />} |
| /follow-board | DELETE | DELETE /follow-board<br />Unfollow board:<br />{<br />    'boardname': boardname, <br />} |
| /follow-board | GET | GET /follow-board<br />Get following board list |


