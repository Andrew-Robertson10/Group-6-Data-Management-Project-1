# 15058 - Group 6 - MIST 4610 Group Project #1 - Music Industry Data Model

The task at hand is to create a model for a database of the music industry, including record labels, artists, songs, albums, awards, concerts, and fans. This database shows how the different entities interact with each other in the world. Each entity has its own unique qualities but is related to other entities in this environment and is used to push the music industry forward. We also demonstrate practical SQL queries for this model to show how it can be used in a real-world context. 


## Authors

- Maxwell Stewart [@maxwellstewart](https://github.com/maxwellstewart)
- Andrew Robertson [@Andrew-Robertson10](https://github.com/Andrew-Robertson10)
- Alex Zou [@FireguyZou123](https://github.com/FireguyZou123)
- AJ Willis[@AJWillis172](https://github.com/AJWillis172)
  

## Data Model
Add explanation for the model here
<img width="953" height="875" alt="Image" src="https://github.com/user-attachments/assets/1347cce8-75ab-4eea-95f8-182b9d7928a5" />

## Data Dictionary

## Queries
Query 1 lists each fan's name as well as the names of the artists whose concerts they have attended.
SELECT fanName, artistName
FROM Fan
JOIN ConcertsAttended ON ConcertsAttended.fanID = Fan.fanID
JOIN Concert ON ConcertsAttended.date(s) = Concert.date(s) AND ConcertsAttended.startTime Concert.startTime AND ConcertsAttended.endTime = Concert.endTime
JOIN Artist ON Concert.artistID = Artist.ArtistID;

This query is useful for determining which artists a fan likes the most and displaying the results in an easy-to-read format. If someone has attended an artist's concert, it is logical to assume that they love that artist more than the average fan. This information can be useful for targeting advertisements, new music releases, and merchandise by the artist.

Query 2 
Lists each album’s ID and title, the album’s primary artist, and the number of songs on that album, returning only albums that contain at least one song and ordering results from most tracks to fewest. 
SELECT Album.albumID, Album.albumName, Artist.artistName,COUNT(Song.songID) AS song_count
FROM Album 
JOIN Artist ON Artist.artistID = Album.artistID 
JOIN Song ON Song.albumID = Album.albumID 
GROUP BY Album.albumID, Album.albumName, Artist.artistName 
ORDER BY song_count DESC;

This query reveals which albums have the largest tracklists so product, marketing, and A&R(Artists and Repertoire) teams can prioritize releases for deluxe editions, bundle or promotion opportunities. It also helps identify albums with high track counts that may warrant additional marketing investment.



## Database Information

