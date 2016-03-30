# local-test-result
0. friends/uuid GET works returns  
 

		{
		  "detail": "Authentication credentials were not provided."
		}

	if no authentication is provided works on master

1. friends/uuid POST works on master
	request body:

		{
			"query":"friends",
			"author":"8cf7c6c3-a3ab-4e58-bd9a-518a71861db6",
			"authors": [
			    "de305d54-75b4-431b-adb2-eb6b9e546013",
				"2dbcdb76-f249-4f48-9601-4c4b7e002678",
				"81a84efa-d362-4bb2-b748-ff89e93c18ae"
		  	]
		}

	response: 

		{
		  "query": "friends",
		  "author": "8cf7c6c3-a3ab-4e58-bd9a-518a71861db6",
		  "authors": [
		    "2dbcdb76-f249-4f48-9601-4c4b7e002678"
		  ]
		}

2. friends/uuid GET returns

		{
		  "query": "friends",
		  "author": "8cf7c6c3-a3ab-4e58-bd9a-518a71861db6",
		  "authors": [
		    "2dbcdb76-f249-4f48-9601-4c4b7e002678"
		  ]
		}

3. friends/uuid GET returns 

		{
		  "detail": "Authentication credentials were not provided."
		}

	if no authentication is provided


4. friends/uuid/uuid GET returns

		{
		  "detail": "Authentication credentials were not provided."
		}
		
	if no authentication is provided
	
5. friends/uuid/uuid GET returns 

		{
		  "query": "friends",
		  "author": "8cf7c6c3-a3ab-4e58-bd9a-518a71861db6",
		  "authors": [
		    "2dbcdb76-f249-4f48-9601-4c4b7e002678"
		  ]
		}
		
	works on master

6. friendrequest/ works when body is

		{
			"query":"friendrequest",
			"author": {
				"id":"face4efa-d362-4bb2-b748-ff89e93c18ae",
				"host":"fakehost.com",
				"displayName":"remote author"
			},
			"friend": {
				"id":"8cf7c6c3-a3ab-4e58-bd9a-518a71861db6",
				"host":"127.0.0.1:8000",
				"displayName":"qiang1",
				"url":"http://127.0.0.1:8000/api/author/8cf7c6c3-a3ab-4e58-bd9a-518a71861db6/"
			}
		}

	and follow relationship is 
	
		    {
		        "url": "http://127.0.0.1:8000/api/follow/3/",
		        "followed": "http://127.0.0.1:8000/api/author/8cf7c6c3-a3ab-4e58-bd9a-518a71861db6/",
		        "follower": null,
		        "remote_author_id": "face4efa-d362-4bb2-b748-ff89e93c18ae",
		        "remote_author_name": "remote author",
		        "remote_author_url": "fakehost.comface4efa-d362-4bb2-b748-ff89e93c18ae",
		        "remote_author_host": "fakehost.com"
		    }
    
    works on master

7. Internal API test: 
	a. api/follower/uuid/remoteauthorfollowers GET

		[
		  {
		    "url": "http://127.0.0.1:8000/api/follow/4/",
		    "followed": null,
		    "follower": "http://127.0.0.1:8000/api/author/8cf7c6c3-a3ab-4e58-bd9a-518a71861db6/",
		    "remote_author_id": "face4efa-d362-4bb2-b748-ff89e93c18ae",
		    "remote_author_name": "remote author",
		    "remote_author_url": "http://fakehost.com/api/author/",
		    "remote_author_host": "fakehost.com"
		  },
		  {
		    "url": "http://127.0.0.1:8000/api/follow/5/",
		    "followed": null,
		    "follower": "http://127.0.0.1:8000/api/author/d57e6aa1-1101-4c29-b8ec-6fa9876152f2/",
		    "remote_author_id": "face4efa-d362-4bb2-b748-ff89e93c18ae",
		    "remote_author_name": "remote author",
		    "remote_author_url": "http://fakehost.com/api/author/",
		    "remote_author_host": "fakehost.com"
		  }
		]
		
	b. api/follower/uuid/remoteAuthorFollowings GET
	
		[
		  {
		    "url": "http://127.0.0.1:8000/api/follow/3/",
		    "followed": "http://127.0.0.1:8000/api/author/8cf7c6c3-a3ab-4e58-bd9a-518a71861db6/",
		    "follower": null,
		    "remote_author_id": "face4efa-d362-4bb2-b748-ff89e93c18ae",
		    "remote_author_name": "remote author",
		    "remote_author_url": "fakehost.comface4efa-d362-4bb2-b748-ff89e93c18ae",
		    "remote_author_host": "fakehost.com"
		  }
		]
		
	c. api/follower/uuid/localAuthorFollowings GET
	
		[
		  {
		    "url": "http://127.0.0.1:8000/api/follow/2/",
		    "followed": "http://127.0.0.1:8000/api/author/2dbcdb76-f249-4f48-9601-4c4b7e002678/",
		    "follower": "http://127.0.0.1:8000/api/author/8cf7c6c3-a3ab-4e58-bd9a-518a71861db6/",
		    "remote_author_id": null,
		    "remote_author_name": null,
		    "remote_author_url": null,
		    "remote_author_host": null
		  },
		  {
		    "url": "http://127.0.0.1:8000/api/follow/4/",
		    "followed": null,
		    "follower": "http://127.0.0.1:8000/api/author/8cf7c6c3-a3ab-4e58-bd9a-518a71861db6/",
		    "remote_author_id": "face4efa-d362-4bb2-b748-ff89e93c18ae",
		    "remote_author_name": "remote author",
		    "remote_author_url": "http://fakehost.com/api/author/",
		    "remote_author_host": "fakehost.com"
		  }
		]
		
		both remote and local followed are shown
	d. api/follower/uuid/localAuthorFollowers GET
	
		[
		  {
		    "url": "http://127.0.0.1:8000/api/follow/1/",
		    "followed": "http://127.0.0.1:8000/api/author/8cf7c6c3-a3ab-4e58-bd9a-518a71861db6/",
		    "follower": "http://127.0.0.1:8000/api/author/2dbcdb76-f249-4f48-9601-4c4b7e002678/",
		    "remote_author_id": null,
		    "remote_author_name": null,
		    "remote_author_url": null,
		    "remote_author_host": null
		  },
		  {
		    "url": "http://127.0.0.1:8000/api/follow/3/",
		    "followed": "http://127.0.0.1:8000/api/author/8cf7c6c3-a3ab-4e58-bd9a-518a71861db6/",
		    "follower": null,
		    "remote_author_id": "face4efa-d362-4bb2-b748-ff89e93c18ae",
		    "remote_author_name": "remote author",
		    "remote_author_url": "fakehost.comface4efa-d362-4bb2-b748-ff89e93c18ae",
		    "remote_author_host": "fakehost.com"
		  }
		]
		
		both remote and local followers are shown

		
