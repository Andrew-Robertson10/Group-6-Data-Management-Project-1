# 15058 - Group 6 - MIST 4610 Group Project #1 - Music Industry Data Model

The task at hand is to create a model for a database of the music industry, including record labels, artists, songs, albums, awards, concerts, and fans. This database shows how the different entities interact with each other in the world. Each entity has its own unique qualities but is related to other entities in this environment and is used to push the music industry forward. We also demonstrate practical SQL queries for this model to show how it can be used in a real-world context. 


## Authors

- Maxwell Stewart [@maxwellstewart](https://github.com/maxwellstewart)
- Andrew Robertson [@Andrew-Robertson10](https://github.com/Andrew-Robertson10)
- Alex Zou [@FireguyZou123](https://github.com/FireguyZou123)
- AJ Willis[@AJWillis172](https://github.com/AJWillis172)
- Aakash Parmar [@aakashbparmar](https://github.com/aakashbparmar)
  

## Data Model
Explanation of the Data Model:

Our model is based on the structure of the music entity. The recordLabel entity represents a record label which represents many artists. Therefore, there is a one-to-many relationships between RecordLabel and Artist.

An Artist produces many albums and many songs. Artists can also create collaborations which include a primary artist and secondary artist. The Collaboration entity has two one-to-many relationships with Artist to represent this relationship. Many songs can be collaborations featuring many artists, so Collaboration is used as an associative entity between Song and Artist to represent this relationship.

An Album contains many songs, so there is a one-to-many relationship between Album and Songs.

Albums or separate songs can win awards. The Award entity features one-to-many relationships between Album and Song to represent the albums and songs that win awards. The Award entity also features other details about the award, including its name, year, and category. Some awards such as the Grammys give the same award each year for different categories, such as best new artist, best song of specific genres, and best music video, so this attribute highlights the difference between awards given in these categories.

The Concert entity is identified by the artist's ID, venue's ID, date, start time, and end time. It also features details about the artist lineup if there are secondary artists at the concert.

ConcertsAttended is an associative entity between the many-to-many relationship between Concert and Fan. Many fans can attend many different concerts.

The Fan entity is identified by the fan's unique ID number and includes details about their name and the concert tickets they currently hold. The fan entity is used to keep track of people who attend artists' concerts.

The Venue entity includes details about the venue's location, name, and maximum occupancy. It features a one-to-one relationship with Employee to identify the manager of the venue. It also has a one-to-many relationship with Employee to keep track of all of the employees that work at each venue. Many employees work at one venue, and one employee is designated as the manager of one venue. The Employee attribute features the employee's identifying ID number and details about their name, address, and the venue they work at. Employee also has a recursive one-to-many relationship with itself to identify an employee's supervisor. One employee supervises multiple other employees.


<img width="957" height="875" alt="Image" src="https://github.com/user-attachments/assets/3c520930-4e7b-425d-a297-4b3b1fabb744" />

## Data Dictionary
<img width="932" height="406" alt="Image" src="https://github.com/user-attachments/assets/3475d326-9ebd-4ffa-9dbb-4315dba0e269" />

<img width="925" height="607" alt="Image" src="https://github.com/user-attachments/assets/90ffb5d5-075f-43a4-bec9-9cda05d1f29a" />

<img width="951" height="366" alt="Image" src="https://github.com/user-attachments/assets/9f9c82bb-c6a6-44f2-b0f6-4f03763fc808" />

<img width="638" height="623" alt="Image" src="https://github.com/user-attachments/assets/63b48cd0-4c09-4a89-828f-4b155459a47c" />

<img width="637" height="577" alt="Image" src="https://github.com/user-attachments/assets/730d5d1d-0aff-4e60-b6f0-e32479867b0a" />

<img width="928" height="667" alt="Image" src="https://github.com/user-attachments/assets/e32405f7-6528-4ec2-802f-f8104b5d4f8e" />

<img width="928" height="685" alt="Image" src="https://github.com/user-attachments/assets/f2483075-bf33-4454-985f-7e5bcd2b14da" />

<img width="861" height="447" alt="Image" src="https://github.com/user-attachments/assets/c03a230c-454b-47ec-9fdc-7c97ce309388" />

<img width="827" height="447" alt="Image" src="https://github.com/user-attachments/assets/9eb3fb1d-6d83-4069-8a51-fc47c60d888f" />

<img width="852" height="432" alt="Image" src="https://github.com/user-attachments/assets/b7cbee45-85a1-4819-93a8-ee386500b7c5" />

<img width="836" height="662" alt="Image" src="https://github.com/user-attachments/assets/7c2bc8be-581b-4933-a22b-56d91e6a9f7c" />


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

Query 3
Lists each artist's name, ID, and most-awarded album

SELECT Artist.artistID, Artist.artistName, Album.albumID, Album.albumName, (SELECT COUNT(*) FROM Award WHERE Award.albumID = Album.albumID) AS "Award Count"
FROM Artist
JOIN Album ON Album.artistID = Artist.artistID
WHERE (SELECT COUNT(*) FROM Award WHERE Award.albumID = Album.albumID)
  =
  (
    SELECT MAX(
      (SELECT COUNT(*) FROM Award AS artistawards WHERE artistawards.albumID = albumawards.albumID)
    )
    FROM Album albumawards
    WHERE albumawards.artistID = Artist.artistID
  );

This query is useful for artists and producers to see which album an artist produced was the most popular and critically acclaimed. It can help the artist learn what types of music their fans like and what type of music to make in the future.

## Database Information

