# Introduction to APIs

## Quick Links

* [API Introduction Docs](https://github.com/craigsdennis/intro-to-apis-course/blob/master/course-notes.md)

* [Working with Web APIs (Online Book)](https://launchschool.com/books/working_with_apis)

## Overview
An API (Application Programming Interface) is a way for different machines and software to talk to each other to create ever more complex applications.  It is a contract of sorts: it defines how it is expected to be used and what you can expect to receive by using it.  

When most people hear the acronym API, they most likely are thinking about web-based APIs, which is completely understandable.  You must also know about the many APIs that are built into all modern programming languages.  For example, let's say you wanted to capitalize a string of text.  We could write a long code to translate each individual letter to the uppercase version through low level bitmath OR we could use the uppercase API:

**Python**
```py
'yeet!'.upper() # YEET!
```
**JavaScript**
```js
'yeet!'.toUpperCase(); // YEET!
```
**Java**
```java
"yeet!".toUpperCase(); // YEET!
```
Basically, programmers use APIs to avoid recreating the wheel.  APIs assist us in accomplishing tasks that we need to perform, by abstracting away a ton of work for us.  

## Remote APIs
The above examples we gave were local APIs, built into the programming language.  Remote APIs can be looked at similarly to your TV's remote.  You work with the interface on the remote to make changes to the TV, as if you were using the interface on the device itself.  

Its not just physical objects that benefit from remote APIs.  Sometimes, we don't have space on our local machines for all the data that is available.  For example, when we use an app like Shazam to find out what song is playing, the app doesn't store ALL the songs in the world on your phone; it instead uses a remote API to send data to the app serice for indentification.  

Remote APIs also offer another benefit of computational power.  Because an API removes the limitations of your local machine, you can gain access to huge amounts of computational power.  A good example of this is the AR feature in the Google Translate app.  The app allows you to use the camera on your phone to translate what you are seeing directly to your screen in near real-time.  This app requires a ton of computational power and it is getting it elsewhere (through cloud computing).  

## REST (**RE**presentational **S**tate **T**ransfer)
The struggle to achieve the concept of remote APIs was very real.  The biggest problem was that there was no standard that everyone loved.  Overtime, a clear winner came forward that offered a clean and universally-accepted format, REST.  The popularity of REST spread so rapidly that it nearly took over the word API (think how XEROX almost took over the term photocopy).  REST is not the end-all, be-all of remote APIs, but it is one of the most common and documented solution.  The following notes will cover the REST framework!  

!!! tip "RESTful"
	When APIs embrace the styles and constraints of REST, they are said to be RESTful.

Here are the guiding architectural constraints for an API to be considered RESTful:  

* Client-Server Architecture  

* Statelessness  

* Layered System  

* Cacheability  

* Uniform Design  

* Code on Demand  

Let's cover these topics by discussing how APIs sit on top of web technology.  Much like the web, the client (web browser/program) makes a request to a server.  Your program will most likely be using some type of library to create the request to the server.  The protocol used for these requests are through HTTP and it is stateless (the server won't remember anything about the particular client (state can be maintained through headers)).  

This request was almost certainly requesting information about a resource.  The "resource" is a little absract, it is the **R** in U**R**L or U**R**I.  We use the term resource to reference an object, which is also abstract.  This is because we can use resources to describe just about anything we build.  For example, let's imagine an e-book store website.  Each book available for purchase is a resource. If we click into it,  we may see a link to the author, which is also a resource.  When we click on a resource the browser sends a GET request to the server.  The RESTful API follows the same logic; your program will send a GET request to a URI (Uniform Resource Identifier), then the server responds with data.  The body of the data returned is typically represented today as **JSON** (JavaScript Object Notation).  JSON provides a great way to structure and nest the data.  

Here are a few HTTP verbs that are used in REST APIs to clearly state the intention of your request:

| HTTP Verbs | CRUD (Create, Read, Update, Delete) |
|------------|-------------------------------------|
| GET        | Read                                |
| POST       | Create                              |
| PUT        | Update                              |
| PATCH      | Update                              |
| DELETE     | Delete                              |

Want to add an author?  POST to the /authors and send them the data you want to update in the body of your request:
```json
POST /authors/{author_Name: "Dave Eggers"}
```
Want to remove an author?  Send a DELETE to that specific author:
```json
DELETE /authors/{HBWSG123}
```  
This means that you can interact with any application out there that exposes their REST API.  

## Exploring an API Online
Let's look at a real API online and see what we can learn.  For this, we are going to be looking at Spotify's [API](https://developer.spotify.com/discover).  Here we can see all the different features that Spotify allows user's to use in their API.  Let's go down to the Search section and read the [documentation](https://developer.spotify.com/documentation/web-api/reference/search/search/).  We can click on the API beta link at the top and then look for the ["Search for an Item"](https://developer.spotify.com/documentation/web-api/reference-beta/#endpoint-search) link.  This documentation explains the "contract" of what we need to do in order to use the API.  

In this documentation we can see which type of headers and query parameters in the request are required or optional for the API to work.  You can also see the types of reponses your request can receive.  Reading the documentation for APIs is perhaps the most important step in implementing an API in your code.  You will see notes from the programmers on how to actually make it work!  

Let's work with Spotify's [Web Console](https://developer.spotify.com/console/get-search-item/), which allows us to test their APIs and play around with the different features.  The Console will show us where it will query:
```
GET https://api.spotify.com/v1/search
```  
and how it will query:
```
curl -X "GET" "https://api.spotify.com/v1/search?q=Palace&type=artist&market=US&limit=2" -H "Accept: application/json" -H "Content-Type: application/json" -H "Authorization: Bearer BQBBI2LYRwSAZ__Agy0GV0BU_i3adk4b4Wsv7eQbfsgdOJUn0HJDgCJpF3v6g_oJ6rcZjOeEdVVz4FrIKZWoAixqhEhJYtqByw0jQfC5ZMHq-wqJACdyrQ7sIQlpeZXemL2jGhfa728ckA9"
```
If we break down the above API GET request, we can see that we are searching for `?q=Palace&type=artist` along with some other bits.  I have limited the results to 2 (`&limit=2`) in order to keep the result set small.  You can also see the Bearer OAuth token at the end, which I have changed in order for my account to remain anonymous.  

If we run this in the Console, we will get a result that looks something like the following:
```json
{
  "artists": {
    "href": "https://api.spotify.com/v1/search?query=Palace&type=artist&market=US&offset=0&limit=2",
    "items": [
      {
        "external_urls": {
          "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
        },
        "followers": {
          "href": null,
          "total": 107224
        },
        "genres": [
          "english indie rock",
          "indie soul",
          "vapor soul"
        ],
        "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
        "id": "48vDIufGC8ujPuBiTxY8dm",
        "images": [
          {
            "height": 640,
            "url": "https://i.scdn.co/image/8b76736404ceb4bc72669f44908dea557ab03083",
            "width": 640
          },
          {
            "height": 320,
            "url": "https://i.scdn.co/image/0c135b9e55b911a37b7aee00af60630c777d4c04",
            "width": 320
          },
          {
            "height": 160,
            "url": "https://i.scdn.co/image/79c30a9ba1518749fb74cc449bcaa060f8aa8151",
            "width": 160
          }
        ],
        "name": "Palace",
        "popularity": 59,
        "type": "artist",
        "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
      },
      {
        "external_urls": {
          "spotify": "https://open.spotify.com/artist/37J1PlAkhRK7yrZUtqaUpQ"
        },
        "followers": {
          "href": null,
          "total": 716429
        },
        "genres": [
          "electro swing",
          "nu jazz"
        ],
        "href": "https://api.spotify.com/v1/artists/37J1PlAkhRK7yrZUtqaUpQ",
        "id": "37J1PlAkhRK7yrZUtqaUpQ",
        "images": [
          {
            "height": 640,
            "url": "https://i.scdn.co/image/adc8c619e766119fabd784a257d6376a653d41ea",
            "width": 640
          },
          {
            "height": 320,
            "url": "https://i.scdn.co/image/65df61829bfdb02f7e068de1b3c28799bdc5ace6",
            "width": 320
          },
          {
            "height": 160,
            "url": "https://i.scdn.co/image/e86351da17029aa21616d98104bbc6f3c61109d7",
            "width": 160
          }
        ],
        "name": "Caravan Palace",
        "popularity": 67,
        "type": "artist",
        "uri": "spotify:artist:37J1PlAkhRK7yrZUtqaUpQ"
      }
    ],
    "limit": 2,
    "next": "https://api.spotify.com/v1/search?query=Palace&type=artist&market=US&offset=2&limit=2",
    "offset": 0,
    "previous": null,
    "total": 448
  }
}
```
Above you can see the response from the Search API of Spotify.  There is some interesting information in here, including the artists unique artist identifier (`48vDIufGC8ujPuBiTxY8dm` for my favorite band Palace), as well as the popularity, folowers, genres, and links to images.  Let's take that artist id and plug it into the "Get an Artist's Top Tracks" API.  

Here we can see that the API URL has changed to:
```
https://api.spotify.com/v1/artists/{id}/top-tracks
```
Let's plug in Palace's artist id into the API call:
```
curl -X "GET" "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm/top-tracks?country=US" -H "Accept: application/json" -H "Content-Type: application/json" -H "Authorization: Bearer BQBBI2LYRwSAZ__Agy0GV0BU_i3adk4b4Wsv7eQbfsgdOJUn0HJDgCJpF3v6g_oJ6rcZjOeEdVVz4FrIKZWoAixqhEhJYtqByw0jQfC5ZMHq-wqJACdyrQ7sIQlpeZZXemL2jGhfa728ckA9"
```
We should get the following resutl:
??? tip "JSON Response"
	```json
	{
	  "tracks": [
	    {
	      "album": {
	        "album_type": "album",
	        "artists": [
	          {
	            "external_urls": {
	              "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	            },
	            "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	            "id": "48vDIufGC8ujPuBiTxY8dm",
	            "name": "Palace",
	            "type": "artist",
	            "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	          }
	        ],
	        "external_urls": {
	          "spotify": "https://open.spotify.com/album/6cmFNl8lllA6BGc7SKLy3y"
	        },
	        "href": "https://api.spotify.com/v1/albums/6cmFNl8lllA6BGc7SKLy3y",
	        "id": "6cmFNl8lllA6BGc7SKLy3y",
	        "images": [
	          {
	            "height": 640,
	            "url": "https://i.scdn.co/image/ab67616d0000b273929dae46c6b93942c7499b7d",
	            "width": 640
	          },
	          {
	            "height": 300,
	            "url": "https://i.scdn.co/image/ab67616d00001e02929dae46c6b93942c7499b7d",
	            "width": 300
	          },
	          {
	            "height": 64,
	            "url": "https://i.scdn.co/image/ab67616d00004851929dae46c6b93942c7499b7d",
	            "width": 64
	          }
	        ],
	        "name": "So Long Forever",
	        "release_date": "2016-11-04",
	        "release_date_precision": "day",
	        "total_tracks": 11,
	        "type": "album",
	        "uri": "spotify:album:6cmFNl8lllA6BGc7SKLy3y"
	      },
	      "artists": [
	        {
	          "external_urls": {
	            "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	          },
	          "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	          "id": "48vDIufGC8ujPuBiTxY8dm",
	          "name": "Palace",
	          "type": "artist",
	          "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	        }
	      ],
	      "disc_number": 1,
	      "duration_ms": 249840,
	      "explicit": false,
	      "external_ids": {
	        "isrc": "GBUM71603029"
	      },
	      "external_urls": {
	        "spotify": "https://open.spotify.com/track/2H30WL3exSctlDC9GyRbD4"
	      },
	      "href": "https://api.spotify.com/v1/tracks/2H30WL3exSctlDC9GyRbD4",
	      "id": "2H30WL3exSctlDC9GyRbD4",
	      "is_local": false,
	      "is_playable": true,
	      "name": "Live Well",
	      "popularity": 64,
	      "preview_url": "https://p.scdn.co/mp3-preview/516b9622373316d4ebbfd4baab240a8217b01952?cid=774b29d4f13844c495f206cafdad9c86",
	      "track_number": 3,
	      "type": "track",
	      "uri": "spotify:track:2H30WL3exSctlDC9GyRbD4"
	    },
	    {
	      "album": {
	        "album_type": "album",
	        "artists": [
	          {
	            "external_urls": {
	              "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	            },
	            "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	            "id": "48vDIufGC8ujPuBiTxY8dm",
	            "name": "Palace",
	            "type": "artist",
	            "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	          }
	        ],
	        "external_urls": {
	          "spotify": "https://open.spotify.com/album/2gnr57XaEBXSDlfbkowBP8"
	        },
	        "href": "https://api.spotify.com/v1/albums/2gnr57XaEBXSDlfbkowBP8",
	        "id": "2gnr57XaEBXSDlfbkowBP8",
	        "images": [
	          {
	            "height": 640,
	            "url": "https://i.scdn.co/image/ab67616d0000b273287d57f51a9220e1b972d576",
	            "width": 640
	          },
	          {
	            "height": 300,
	            "url": "https://i.scdn.co/image/ab67616d00001e02287d57f51a9220e1b972d576",
	            "width": 300
	          },
	          {
	            "height": 64,
	            "url": "https://i.scdn.co/image/ab67616d00004851287d57f51a9220e1b972d576",
	            "width": 64
	          }
	        ],
	        "name": "Life After",
	        "release_date": "2019-07-12",
	        "release_date_precision": "day",
	        "total_tracks": 11,
	        "type": "album",
	        "uri": "spotify:album:2gnr57XaEBXSDlfbkowBP8"
	      },
	      "artists": [
	        {
	          "external_urls": {
	            "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	          },
	          "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	          "id": "48vDIufGC8ujPuBiTxY8dm",
	          "name": "Palace",
	          "type": "artist",
	          "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	        }
	      ],
	      "disc_number": 1,
	      "duration_ms": 437577,
	      "explicit": false,
	      "external_ids": {
	        "isrc": "GBUM71806918"
	      },
	      "external_urls": {
	        "spotify": "https://open.spotify.com/track/3Rl26h1HiMCV0HFHHVb2IM"
	      },
	      "href": "https://api.spotify.com/v1/tracks/3Rl26h1HiMCV0HFHHVb2IM",
	      "id": "3Rl26h1HiMCV0HFHHVb2IM",
	      "is_local": false,
	      "is_playable": true,
	      "name": "Heaven Up There",
	      "popularity": 58,
	      "preview_url": "https://p.scdn.co/mp3-preview/9bfd400bc1701508933e11dd88edbaa3743e726e?cid=774b29d4f13844c495f206cafdad9c86",
	      "track_number": 11,
	      "type": "track",
	      "uri": "spotify:track:3Rl26h1HiMCV0HFHHVb2IM"
	    },
	    {
	      "album": {
	        "album_type": "album",
	        "artists": [
	          {
	            "external_urls": {
	              "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	            },
	            "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	            "id": "48vDIufGC8ujPuBiTxY8dm",
	            "name": "Palace",
	            "type": "artist",
	            "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	          }
	        ],
	        "external_urls": {
	          "spotify": "https://open.spotify.com/album/6cmFNl8lllA6BGc7SKLy3y"
	        },
	        "href": "https://api.spotify.com/v1/albums/6cmFNl8lllA6BGc7SKLy3y",
	        "id": "6cmFNl8lllA6BGc7SKLy3y",
	        "images": [
	          {
	            "height": 640,
	            "url": "https://i.scdn.co/image/ab67616d0000b273929dae46c6b93942c7499b7d",
	            "width": 640
	          },
	          {
	            "height": 300,
	            "url": "https://i.scdn.co/image/ab67616d00001e02929dae46c6b93942c7499b7d",
	            "width": 300
	          },
	          {
	            "height": 64,
	            "url": "https://i.scdn.co/image/ab67616d00004851929dae46c6b93942c7499b7d",
	            "width": 64
	          }
	        ],
	        "name": "So Long Forever",
	        "release_date": "2016-11-04",
	        "release_date_precision": "day",
	        "total_tracks": 11,
	        "type": "album",
	        "uri": "spotify:album:6cmFNl8lllA6BGc7SKLy3y"
	      },
	      "artists": [
	        {
	          "external_urls": {
	            "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	          },
	          "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	          "id": "48vDIufGC8ujPuBiTxY8dm",
	          "name": "Palace",
	          "type": "artist",
	          "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	        }
	      ],
	      "disc_number": 1,
	      "duration_ms": 233360,
	      "explicit": false,
	      "external_ids": {
	        "isrc": "GBUM71603022"
	      },
	      "external_urls": {
	        "spotify": "https://open.spotify.com/track/2DkZisoN9h1dLa8Sn5sx0n"
	      },
	      "href": "https://api.spotify.com/v1/tracks/2DkZisoN9h1dLa8Sn5sx0n",
	      "id": "2DkZisoN9h1dLa8Sn5sx0n",
	      "is_local": false,
	      "is_playable": true,
	      "name": "Bitter",
	      "popularity": 58,
	      "preview_url": "https://p.scdn.co/mp3-preview/df18b5b91c3b46589dc1bbca26fbdfd895028995?cid=774b29d4f13844c495f206cafdad9c86",
	      "track_number": 2,
	      "type": "track",
	      "uri": "spotify:track:2DkZisoN9h1dLa8Sn5sx0n"
	    },
	    {
	      "album": {
	        "album_type": "single",
	        "artists": [
	          {
	            "external_urls": {
	              "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	            },
	            "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	            "id": "48vDIufGC8ujPuBiTxY8dm",
	            "name": "Palace",
	            "type": "artist",
	            "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	          }
	        ],
	        "external_urls": {
	          "spotify": "https://open.spotify.com/album/161a4wcY3Lh9xN8OEF0RMr"
	        },
	        "href": "https://api.spotify.com/v1/albums/161a4wcY3Lh9xN8OEF0RMr",
	        "id": "161a4wcY3Lh9xN8OEF0RMr",
	        "images": [
	          {
	            "height": 640,
	            "url": "https://i.scdn.co/image/ab67616d0000b27390912ce0aad8b575d3cd1b50",
	            "width": 640
	          },
	          {
	            "height": 300,
	            "url": "https://i.scdn.co/image/ab67616d00001e0290912ce0aad8b575d3cd1b50",
	            "width": 300
	          },
	          {
	            "height": 64,
	            "url": "https://i.scdn.co/image/ab67616d0000485190912ce0aad8b575d3cd1b50",
	            "width": 64
	          }
	        ],
	        "name": "Someday, Somewhere",
	        "release_date": "2020-07-17",
	        "release_date_precision": "day",
	        "total_tracks": 1,
	        "type": "album",
	        "uri": "spotify:album:161a4wcY3Lh9xN8OEF0RMr"
	      },
	      "artists": [
	        {
	          "external_urls": {
	            "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	          },
	          "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	          "id": "48vDIufGC8ujPuBiTxY8dm",
	          "name": "Palace",
	          "type": "artist",
	          "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	        }
	      ],
	      "disc_number": 1,
	      "duration_ms": 192461,
	      "explicit": false,
	      "external_ids": {
	        "isrc": "GBUM72002794"
	      },
	      "external_urls": {
	        "spotify": "https://open.spotify.com/track/75Ibf9kajH52v2uBNc7pkp"
	      },
	      "href": "https://api.spotify.com/v1/tracks/75Ibf9kajH52v2uBNc7pkp",
	      "id": "75Ibf9kajH52v2uBNc7pkp",
	      "is_local": false,
	      "is_playable": true,
	      "name": "Someday, Somewhere",
	      "popularity": 55,
	      "preview_url": "https://p.scdn.co/mp3-preview/9a45e9861c165c1c653f1f54b9049f7033134bd7?cid=774b29d4f13844c495f206cafdad9c86",
	      "track_number": 1,
	      "type": "track",
	      "uri": "spotify:track:75Ibf9kajH52v2uBNc7pkp"
	    },
	    {
	      "album": {
	        "album_type": "single",
	        "artists": [
	          {
	            "external_urls": {
	              "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	            },
	            "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	            "id": "48vDIufGC8ujPuBiTxY8dm",
	            "name": "Palace",
	            "type": "artist",
	            "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	          }
	        ],
	        "external_urls": {
	          "spotify": "https://open.spotify.com/album/0LyecvMmiD3grsZtkEQQJM"
	        },
	        "href": "https://api.spotify.com/v1/albums/0LyecvMmiD3grsZtkEQQJM",
	        "id": "0LyecvMmiD3grsZtkEQQJM",
	        "images": [
	          {
	            "height": 640,
	            "url": "https://i.scdn.co/image/ab67616d0000b273ca84a453df6f486114bcc774",
	            "width": 640
	          },
	          {
	            "height": 300,
	            "url": "https://i.scdn.co/image/ab67616d00001e02ca84a453df6f486114bcc774",
	            "width": 300
	          },
	          {
	            "height": 64,
	            "url": "https://i.scdn.co/image/ab67616d00004851ca84a453df6f486114bcc774",
	            "width": 64
	          }
	        ],
	        "name": "Veins",
	        "release_date": "2014-07-15",
	        "release_date_precision": "day",
	        "total_tracks": 1,
	        "type": "album",
	        "uri": "spotify:album:0LyecvMmiD3grsZtkEQQJM"
	      },
	      "artists": [
	        {
	          "external_urls": {
	            "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	          },
	          "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	          "id": "48vDIufGC8ujPuBiTxY8dm",
	          "name": "Palace",
	          "type": "artist",
	          "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	        }
	      ],
	      "disc_number": 1,
	      "duration_ms": 269974,
	      "explicit": false,
	      "external_ids": {
	        "isrc": "GBLVL1400017"
	      },
	      "external_urls": {
	        "spotify": "https://open.spotify.com/track/1UsXMQwIzCKSk6oIdRE5Jc"
	      },
	      "href": "https://api.spotify.com/v1/tracks/1UsXMQwIzCKSk6oIdRE5Jc",
	      "id": "1UsXMQwIzCKSk6oIdRE5Jc",
	      "is_local": false,
	      "is_playable": true,
	      "name": "Veins",
	      "popularity": 52,
	      "preview_url": "https://p.scdn.co/mp3-preview/69efa6483c01ab1c3bd323d7a71287aa9b126317?cid=774b29d4f13844c495f206cafdad9c86",
	      "track_number": 1,
	      "type": "track",
	      "uri": "spotify:track:1UsXMQwIzCKSk6oIdRE5Jc"
	    },
	    {
	      "album": {
	        "album_type": "single",
	        "artists": [
	          {
	            "external_urls": {
	              "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	            },
	            "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	            "id": "48vDIufGC8ujPuBiTxY8dm",
	            "name": "Palace",
	            "type": "artist",
	            "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	          }
	        ],
	        "external_urls": {
	          "spotify": "https://open.spotify.com/album/1SJbZWC9jhrR1m4fDYP1ys"
	        },
	        "href": "https://api.spotify.com/v1/albums/1SJbZWC9jhrR1m4fDYP1ys",
	        "id": "1SJbZWC9jhrR1m4fDYP1ys",
	        "images": [
	          {
	            "height": 640,
	            "url": "https://i.scdn.co/image/ab67616d0000b273f490d80a7841c5bd61a4f694",
	            "width": 640
	          },
	          {
	            "height": 300,
	            "url": "https://i.scdn.co/image/ab67616d00001e02f490d80a7841c5bd61a4f694",
	            "width": 300
	          },
	          {
	            "height": 64,
	            "url": "https://i.scdn.co/image/ab67616d00004851f490d80a7841c5bd61a4f694",
	            "width": 64
	          }
	        ],
	        "name": "Bitter",
	        "release_date": "2014-08-11",
	        "release_date_precision": "day",
	        "total_tracks": 1,
	        "type": "album",
	        "uri": "spotify:album:1SJbZWC9jhrR1m4fDYP1ys"
	      },
	      "artists": [
	        {
	          "external_urls": {
	            "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	          },
	          "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	          "id": "48vDIufGC8ujPuBiTxY8dm",
	          "name": "Palace",
	          "type": "artist",
	          "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	        }
	      ],
	      "disc_number": 1,
	      "duration_ms": 234674,
	      "explicit": false,
	      "external_ids": {
	        "isrc": "GBLVL1400014"
	      },
	      "external_urls": {
	        "spotify": "https://open.spotify.com/track/6xxy4SktborcH1wRjISek5"
	      },
	      "href": "https://api.spotify.com/v1/tracks/6xxy4SktborcH1wRjISek5",
	      "id": "6xxy4SktborcH1wRjISek5",
	      "is_local": false,
	      "is_playable": true,
	      "name": "Bitter",
	      "popularity": 48,
	      "preview_url": "https://p.scdn.co/mp3-preview/36eda2cdf0d31e8b694552159d012fc677296af1?cid=774b29d4f13844c495f206cafdad9c86",
	      "track_number": 1,
	      "type": "track",
	      "uri": "spotify:track:6xxy4SktborcH1wRjISek5"
	    },
	    {
	      "album": {
	        "album_type": "single",
	        "artists": [
	          {
	            "external_urls": {
	              "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	            },
	            "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	            "id": "48vDIufGC8ujPuBiTxY8dm",
	            "name": "Palace",
	            "type": "artist",
	            "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	          }
	        ],
	        "external_urls": {
	          "spotify": "https://open.spotify.com/album/50lmuZTx1lNcNFjY2cr3HB"
	        },
	        "href": "https://api.spotify.com/v1/albums/50lmuZTx1lNcNFjY2cr3HB",
	        "id": "50lmuZTx1lNcNFjY2cr3HB",
	        "images": [
	          {
	            "height": 640,
	            "url": "https://i.scdn.co/image/ab67616d0000b273e84adb5bc350142cb67a5656",
	            "width": 640
	          },
	          {
	            "height": 300,
	            "url": "https://i.scdn.co/image/ab67616d00001e02e84adb5bc350142cb67a5656",
	            "width": 300
	          },
	          {
	            "height": 64,
	            "url": "https://i.scdn.co/image/ab67616d00004851e84adb5bc350142cb67a5656",
	            "width": 64
	          }
	        ],
	        "name": "Lost in the Night",
	        "release_date": "2014-10-20",
	        "release_date_precision": "day",
	        "total_tracks": 5,
	        "type": "album",
	        "uri": "spotify:album:50lmuZTx1lNcNFjY2cr3HB"
	      },
	      "artists": [
	        {
	          "external_urls": {
	            "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	          },
	          "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	          "id": "48vDIufGC8ujPuBiTxY8dm",
	          "name": "Palace",
	          "type": "artist",
	          "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	        }
	      ],
	      "disc_number": 1,
	      "duration_ms": 242430,
	      "explicit": false,
	      "external_ids": {
	        "isrc": "GBLVL1400015"
	      },
	      "external_urls": {
	        "spotify": "https://open.spotify.com/track/6wimdClggXbqamkhOsyRQ9"
	      },
	      "href": "https://api.spotify.com/v1/tracks/6wimdClggXbqamkhOsyRQ9",
	      "id": "6wimdClggXbqamkhOsyRQ9",
	      "is_local": false,
	      "is_playable": true,
	      "name": "I Want What You Got",
	      "popularity": 47,
	      "preview_url": "https://p.scdn.co/mp3-preview/9c7ba3c471bfaa2fe5ff68ca87402fa8e65ee80f?cid=774b29d4f13844c495f206cafdad9c86",
	      "track_number": 2,
	      "type": "track",
	      "uri": "spotify:track:6wimdClggXbqamkhOsyRQ9"
	    },
	    {
	      "album": {
	        "album_type": "album",
	        "artists": [
	          {
	            "external_urls": {
	              "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	            },
	            "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	            "id": "48vDIufGC8ujPuBiTxY8dm",
	            "name": "Palace",
	            "type": "artist",
	            "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	          }
	        ],
	        "external_urls": {
	          "spotify": "https://open.spotify.com/album/6cmFNl8lllA6BGc7SKLy3y"
	        },
	        "href": "https://api.spotify.com/v1/albums/6cmFNl8lllA6BGc7SKLy3y",
	        "id": "6cmFNl8lllA6BGc7SKLy3y",
	        "images": [
	          {
	            "height": 640,
	            "url": "https://i.scdn.co/image/ab67616d0000b273929dae46c6b93942c7499b7d",
	            "width": 640
	          },
	          {
	            "height": 300,
	            "url": "https://i.scdn.co/image/ab67616d00001e02929dae46c6b93942c7499b7d",
	            "width": 300
	          },
	          {
	            "height": 64,
	            "url": "https://i.scdn.co/image/ab67616d00004851929dae46c6b93942c7499b7d",
	            "width": 64
	          }
	        ],
	        "name": "So Long Forever",
	        "release_date": "2016-11-04",
	        "release_date_precision": "day",
	        "total_tracks": 11,
	        "type": "album",
	        "uri": "spotify:album:6cmFNl8lllA6BGc7SKLy3y"
	      },
	      "artists": [
	        {
	          "external_urls": {
	            "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	          },
	          "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	          "id": "48vDIufGC8ujPuBiTxY8dm",
	          "name": "Palace",
	          "type": "artist",
	          "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	        }
	      ],
	      "disc_number": 1,
	      "duration_ms": 246893,
	      "explicit": false,
	      "external_ids": {
	        "isrc": "GBUM71602810"
	      },
	      "external_urls": {
	        "spotify": "https://open.spotify.com/track/23uCHFc7xcQWgXh2oelMOe"
	      },
	      "href": "https://api.spotify.com/v1/tracks/23uCHFc7xcQWgXh2oelMOe",
	      "id": "23uCHFc7xcQWgXh2oelMOe",
	      "is_local": false,
	      "is_playable": true,
	      "name": "Have Faith",
	      "popularity": 46,
	      "preview_url": "https://p.scdn.co/mp3-preview/634c490bc66b42bc99b7637b0abfb24b47853214?cid=774b29d4f13844c495f206cafdad9c86",
	      "track_number": 7,
	      "type": "track",
	      "uri": "spotify:track:23uCHFc7xcQWgXh2oelMOe"
	    },
	    {
	      "album": {
	        "album_type": "album",
	        "artists": [
	          {
	            "external_urls": {
	              "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	            },
	            "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	            "id": "48vDIufGC8ujPuBiTxY8dm",
	            "name": "Palace",
	            "type": "artist",
	            "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	          }
	        ],
	        "external_urls": {
	          "spotify": "https://open.spotify.com/album/6cmFNl8lllA6BGc7SKLy3y"
	        },
	        "href": "https://api.spotify.com/v1/albums/6cmFNl8lllA6BGc7SKLy3y",
	        "id": "6cmFNl8lllA6BGc7SKLy3y",
	        "images": [
	          {
	            "height": 640,
	            "url": "https://i.scdn.co/image/ab67616d0000b273929dae46c6b93942c7499b7d",
	            "width": 640
	          },
	          {
	            "height": 300,
	            "url": "https://i.scdn.co/image/ab67616d00001e02929dae46c6b93942c7499b7d",
	            "width": 300
	          },
	          {
	            "height": 64,
	            "url": "https://i.scdn.co/image/ab67616d00004851929dae46c6b93942c7499b7d",
	            "width": 64
	          }
	        ],
	        "name": "So Long Forever",
	        "release_date": "2016-11-04",
	        "release_date_precision": "day",
	        "total_tracks": 11,
	        "type": "album",
	        "uri": "spotify:album:6cmFNl8lllA6BGc7SKLy3y"
	      },
	      "artists": [
	        {
	          "external_urls": {
	            "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	          },
	          "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	          "id": "48vDIufGC8ujPuBiTxY8dm",
	          "name": "Palace",
	          "type": "artist",
	          "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	        }
	      ],
	      "disc_number": 1,
	      "duration_ms": 305040,
	      "explicit": false,
	      "external_ids": {
	        "isrc": "GBUM71603024"
	      },
	      "external_urls": {
	        "spotify": "https://open.spotify.com/track/0s2mDwSz2RvcHE3DYhSkL2"
	      },
	      "href": "https://api.spotify.com/v1/tracks/0s2mDwSz2RvcHE3DYhSkL2",
	      "id": "0s2mDwSz2RvcHE3DYhSkL2",
	      "is_local": false,
	      "is_playable": true,
	      "name": "So Long Forever",
	      "popularity": 45,
	      "preview_url": "https://p.scdn.co/mp3-preview/257b17e1ea6c76bce48e02bdf416c8c6600a65e8?cid=774b29d4f13844c495f206cafdad9c86",
	      "track_number": 8,
	      "type": "track",
	      "uri": "spotify:track:0s2mDwSz2RvcHE3DYhSkL2"
	    },
	    {
	      "album": {
	        "album_type": "album",
	        "artists": [
	          {
	            "external_urls": {
	              "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	            },
	            "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	            "id": "48vDIufGC8ujPuBiTxY8dm",
	            "name": "Palace",
	            "type": "artist",
	            "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	          }
	        ],
	        "external_urls": {
	          "spotify": "https://open.spotify.com/album/6cmFNl8lllA6BGc7SKLy3y"
	        },
	        "href": "https://api.spotify.com/v1/albums/6cmFNl8lllA6BGc7SKLy3y",
	        "id": "6cmFNl8lllA6BGc7SKLy3y",
	        "images": [
	          {
	            "height": 640,
	            "url": "https://i.scdn.co/image/ab67616d0000b273929dae46c6b93942c7499b7d",
	            "width": 640
	          },
	          {
	            "height": 300,
	            "url": "https://i.scdn.co/image/ab67616d00001e02929dae46c6b93942c7499b7d",
	            "width": 300
	          },
	          {
	            "height": 64,
	            "url": "https://i.scdn.co/image/ab67616d00004851929dae46c6b93942c7499b7d",
	            "width": 64
	          }
	        ],
	        "name": "So Long Forever",
	        "release_date": "2016-11-04",
	        "release_date_precision": "day",
	        "total_tracks": 11,
	        "type": "album",
	        "uri": "spotify:album:6cmFNl8lllA6BGc7SKLy3y"
	      },
	      "artists": [
	        {
	          "external_urls": {
	            "spotify": "https://open.spotify.com/artist/48vDIufGC8ujPuBiTxY8dm"
	          },
	          "href": "https://api.spotify.com/v1/artists/48vDIufGC8ujPuBiTxY8dm",
	          "id": "48vDIufGC8ujPuBiTxY8dm",
	          "name": "Palace",
	          "type": "artist",
	          "uri": "spotify:artist:48vDIufGC8ujPuBiTxY8dm"
	        }
	      ],
	      "disc_number": 1,
	      "duration_ms": 198013,
	      "explicit": false,
	      "external_ids": {
	        "isrc": "GBUM71603030"
	      },
	      "external_urls": {
	        "spotify": "https://open.spotify.com/track/3SJI20YW5l5Ri1etVIx1Vo"
	      },
	      "href": "https://api.spotify.com/v1/tracks/3SJI20YW5l5Ri1etVIx1Vo",
	      "id": "3SJI20YW5l5Ri1etVIx1Vo",
	      "is_local": false,
	      "is_playable": true,
	      "name": "Holy Smoke",
	      "popularity": 45,
	      "preview_url": "https://p.scdn.co/mp3-preview/636cebb17ae17e216bfb39cb276ba29a21003ffb?cid=774b29d4f13844c495f206cafdad9c86",
	      "track_number": 10,
	      "type": "track",
	      "uri": "spotify:track:3SJI20YW5l5Ri1etVIx1Vo"
	    }
	  ]
	}
	```

Here we can see information about their top songs, including name, release date, total tracks, type, direct URI, if it is explicit, the popularity, the track number, and much more.  It even includes a link to a [preview URL](https://p.scdn.co/mp3-preview/636cebb17ae17e216bfb39cb276ba29a21003ffb?cid=774b29d4f13844c495f206cafdad9c86)!  This is a great example of a layered system because the results are not rendered on every request!  The results can be cached because artist data doesn't update very often.  

## Using an API from the Command Line
Let's try making an API request from our own command line, not a website!  Let's use a different API this time, one from [Twilio](https://www.twilio.com/).  We will be working with the "Programmable Messaging" API.  Let's click on "build" and try sending a message to our phone number from the website.  We can do this by adding whatever we want in the "Body" section and then clicking on "Make Request".  You should now receive a text message with whatever you wrote.  

Let's take this a step further and open a terminal.  Let's make a Python program first to interact with this API and send the message:
```py
from twilio.rest import Client 
 
account_sid = 'AC504e58232220f1698dbf3c144af87g2z' #these have been changed for security
auth_token = '261209ecabd9de3cec413a4b458a423zaw' 
client = Client(account_sid, auth_token) 
 
message = client.messages.create( 
                              from_='+12057654321',        
                              to='+19091234567' 
                          ) 
 
print(message.sid)
```
After running the above Python program, we should get a response like:
```json
{
    "sid": "SM55d7040dd06b4c33a19b38863843acea",
    "date_created": "Wed, 02 Sep 2020 17:41:14 +0000",
    "date_updated": "Wed, 02 Sep 2020 17:41:14 +0000",
    "date_sent": null,
    "account_sid": "AC504e58232220f1698dbf3c55a8ff73jm",
    "to": "+19091234567",
    "from": "+12057654321",
    "messaging_service_sid": null,
    "body": "Sent from your Twilio trial account - Hello!",
    "status": "queued",
    "num_segments": "1",
    "num_media": "0",
    "direction": "outbound-api",
    "api_version": "2010-04-01",
    "price": null,
    "price_unit": "USD",
    "error_code": null,
    "error_message": null,
    "uri": "/2010-04-01/Accounts/AC504e58232220f1698dbf3c55a8ff73jm/Messages/SM55d7040dd06b4c33a19b38863843acea.json",
    "subresource_uris": {
        "media": "/2010-04-01/Accounts/AC504e58232220f1698dbf3c55a8ff73jm/Messages/SM55d7040dd06b4c33a19b38863843acea/Media.json"
    }
}
```
Or an error message telling you what went wrong.  

We can also do this as a cURL command:
```curl
curl 'https://api.twilio.com/2010-04-01/Accounts/AC504e58232220f1698dbf3c55a8ff73jm/Messages.json' -X POST \
--data-urlencode 'To=+19091234567' \
--data-urlencode 'From=+12057654321' \
--data-urlencode 'Body=Hello!' \
-u AC504e58232220f1698dbf3c115a8ggt52:[AuthToken]
``` 

If it worked, you should see the message pop up on a verifed phone!
 
## Using Postman to Explore APIs
[Postman](https://www.postman.com/) is a feature rich tool that helps users explore new APIs.  We can use either the browser application or the desktop application for the following.  Let's click on "Create a New Collection", which keeps all request that we make grouped together.  Let's recreate the calls we made to the Twilio API from above.  Let's name the collection "Twilio" and click "Create".  It should now show up in the collections area on the left sidebar.  Click on the Twilio collection and then "Add requests".  We can name the Request "Message Log", and add a descriptive description like the following:
```
All messages sent from my account.  

[Twilio Documentation](https://www.twilio.com/docs/sms/api/message-resource?code-sample=code-read-list-all-messages&code-language=Node.js&code-sdk-version=3.x)
```
It is best practice to reference to the parent documentation whenever using an API for ease of access.  

Now, let's click on the new `GET` request we have created to open it in the Launchpad.  We can now grab the URL from the Twilio cURL `GET` request from earlier:
```
https://api.twilio.com/2010-04-01/Accounts/AC504e58232220f1698dbf3c55a8ff73jm/Messages.json
```
Before we click "Send", we need to make sure we include our auth for Twilio in the "Authorization" in Postman.  We also need to add some variables in the "Variables" tab, specifically `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`.  We can now use these variables in the authorization tab with {{TWILIO_ACCOUNT_SID}} in the username field and {{TWILIO_AUTH_TOKEN}} in the password field.  Now let's click "Send".  

We should get a response with an array filled out will our previous message body, to/from info, date/time, etc.    

### POST Request on Postman
Let's create another request within the Twilio collection titled "Create a message".  Remember to put a description with a link to the documentation!  After creating the request, let's open it and change `GET` to `POST` in the dropdown menu.  We will need to look through the documentation on how to implement this request and make it follow the API's rules.  First, ets fill in the URL:
```
https://api.twilio.com/2010-04-01/Accounts/{{TWILIO_ACCOUNT_SID}}/Messages.json
```
Notice how we used the `{{TWILIO_ACCOUNT_SID}}` instead of the long id from the last request we made.  Now in the Body tab, lets add a `to` key with a value of the number you want to message.  Next, let's create a `body` key with whatever text you want to be sent.  We also need to add a `from` key with our `{{TWILIO_NUMBER}}` (we can add this to the credentials tab).  Now when we click "Send", a message should be sent to the verified number of your choice.  

## Using Helper Libraries (JavaScript)
In order to avoid writing repitive code, we can use helper libraries or SDKs Software Development Kits).  SDKs are unique to each programming language and help make your code more concise and legible.  

We are going to start out by working with [Node](https://nodejs.org/en/).  Node.js is an open-source, cross-platform, JavaScript runtime environment that executes JavaScript code outside of a web browser.  After installing Node, we can open a command prompt and type in the command `node -v` to check what version of Node is loaded.  If an error occurs, Node is not installed properly on your machine.  First, let's create a new directory to work inside with the `mkdir scratch` command.  In that directory let's make a directory called `javascript` with the `mkdir javascript` command.  Lets open this folder in Visual Studio code and create a new file called `explore.js` in the javascript folder.  


