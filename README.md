# Group 6 - MIST 4610 Group Project #1 - Music Industry Data Model

The task at hand is to create a model for a database of the music industry, including record labels, artists, songs, albums, awards, concerts, and fans. This database shows how the different entities interact with each other in the world. Each entity has its own unique qualities but is related to other entities in this environment and is used to push the music industry forward. We also demonstrate practical SQL queries for this model to show how it can be used in a real-world context. 


## Authors

- Maxwell Stewart [@maxwellstewart](https://github.com/maxwellstewart)
- Andrew Robertson [@Andrew-Robertson10](https://github.com/Andrew-Robertson10)
- Alex Zou [@FireguyZou123](https://github.com/FireguyZou123)
- AJ Willis[@AJWillis172](https://github.com/AJWillis172)
  

## Data Model
<img width="940" height="861" alt="Image" src="https://github.com/user-attachments/assets/76d8f2e7-ad9d-4234-872c-bcb6a5660ee6" />

## Data Dictionary

## Queries
Query 1 lists each fan's name as well as the names of the artists whose concerts they have attended.
SELECT fanName, artistName
FROM Fan
JOIN ConcertsAttended ON ConcertsAttended.fanID = Fan.fanID
JOIN Concert ON ConcertsAttended.date(s) = Concert.date(s) AND ConcertsAttended.startTime Concert.startTime AND ConcertsAttended.endTime = Concert.endTime
JOIN Artist ON Concert.artistID = Artist.ArtistID;

This query is useful for determining which artists a fan likes the most and displaying the results in an easy-to-read format. If someone has attended an artist's concert, it is logical to assume that they love that artist more than the average fan. This information can be useful for targeting advertisements, new music releases, and merchandise by the artist.
