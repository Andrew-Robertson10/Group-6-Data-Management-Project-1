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

<img width="957" height="875" alt="Image" src="https://github.com/user-attachments/assets/73da4a26-3b69-440e-9ae0-b01ae2cac226" />

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

<img width="815" height="691" alt="Image" src="https://github.com/user-attachments/assets/4a39f47c-0fec-4310-960d-d06ba377b6c5" />


## Queries
Query 1 lists each fan's name as well as the names of the artists whose concerts they have attended.
```
Execute:
> SELECT fanName, artistName
FROM Fan
JOIN ConcertsAttended ON ConcertsAttended.fanID = Fan.fanID
JOIN Concert ON ConcertsAttended.date = Concert.date AND ConcertsAttended.startTime = Concert.startTime AND ConcertsAttended.endTime = Concert.endTime
JOIN Artist ON Concert.headlinerArtistID = Artist.ArtistID

+ ------------ + --------------- +
| fanName      | artistName      |
+ ------------ + --------------- +
| Xerxes Weedall | Taylor Swift    |
| Hilario Forsythe | Taylor Swift    |
| Morie Risdale | Taylor Swift    |
| Noel Kubiak  | Taylor Swift    |
| Anabel Pywell | Taylor Swift    |
| Layne Lofts  | Taylor Swift    |
| Raul Gillyett | Taylor Swift    |
| Noble Regan  | Taylor Swift    |
| Kris Mingay  | Taylor Swift    |
| Estevan Simmans | Taylor Swift    |
| Deni Bugbird | Ed Sheeran      |
| Selestina Reisen | Ed Sheeran      |
| Dionne Keaveny | Ed Sheeran      |
| Minny Tungate | Ed Sheeran      |
| Anabel Pywell | Lady Gaga       |
| Kacey Grayson | Lady Gaga       |
| Bary Halfacree | Lady Gaga       |
| Marcie Wenger | Lady Gaga       |
| Bary Halfacree | Justin Bieber   |
| Christean O'Riordan | Justin Bieber   |
| Denise Bugdale | Justin Bieber   |
| Jamie Slaght | Justin Bieber   |
| Beatrice Snel | Justin Bieber   |
| L;urette Izacenko | Justin Bieber   |
| Katerine Dullaghan | Justin Bieber   |
| Dionne Keaveny | Justin Bieber   |
| Selinda Addenbrooke | Justin Bieber   |
| Joanie Abbots | Justin Bieber   |
| Belicia Lillicrop | Justin Bieber   |
| Beltran Myles | Katy Perry      |
| Bary Halfacree | Katy Perry      |
| Lowe Traynor | Katy Perry      |
| Scotti Crowche | Katy Perry      |
| Karlotta Montfort | Katy Perry      |
| Burr Dunckley | Katy Perry      |
| Marillin Winkless | Katy Perry      |
| Tedd Eaglen  | Katy Perry      |
| Rhiamon Grigolli | Katy Perry      |
| Efren Sutherns | Katy Perry      |
| Eirena Middler | Katy Perry      |
| Nettie Heintze | Katy Perry      |
| Beltran Myles | Bruno Mars      |
| Rhiamon Ceccoli | Bruno Mars      |
| Auria Simeoni | Bruno Mars      |
| Joanie Abbots | Bruno Mars      |
| Estevan Simmans | Bruno Mars      |
| Gerhardt Keaves | Bruno Mars      |
| Marisa Halwell | Bruno Mars      |
| L;urette Izacenko | Bruno Mars      |
| Neila Perch  | Bruno Mars      |
| Tyrus Manuel | Bruno Mars      |
| Elie Goad    | Bruno Mars      |
| Kermie D'Almeida | Bruno Mars      |
| Even Battle  | Bruno Mars      |
| Lenka Travers | Bruno Mars      |
| Milton Arkow | Bruno Mars      |
| Dania Budget | Bruno Mars      |
| Ronni Quodling | Bruno Mars      |
| Berke Oaker  | Bruno Mars      |
| Pennie Piddington | Bruno Mars      |
| Marcelle Hancock | Bruno Mars      |
| Winni Espadero | Bruno Mars      |
| Shalna Ateridge | Bruno Mars      |
| Jaye Trosdall | Bruno Mars      |
| Rheta Benes  | Bruno Mars      |
| Dania Budget | Bruno Mars      |
| Joelynn Tilby | Bruno Mars      |
| Morie Risdale | Bruno Mars      |
| Karlotta Montfort | Bruno Mars      |
| Bary Halfacree | Adele           |
| Orelie Trinbey | Adele           |
| Dallas Tidbald | Adele           |
| Rey Hammersley | Adele           |
| Denise Bugdale | Adele           |
| Alberta McGruar | Adele           |
| Flore Storck | Adele           |
| Carol-jean Lewsley | Adele           |
| Christean O'Riordan | Adele           |
| Jeffry Ricart | Adele           |
| Clari Gymblett | Adele           |
| Arabelle Curness | Adele           |
| Stella Tills | Adele           |
| Joellyn Lamplough | Nicki Minaj     |
| Linnie Ponnsett | Nicki Minaj     |
| Rica Lawford | Nicki Minaj     |
| Murry Benion | Nicki Minaj     |
| Brigida Spratling | Nicki Minaj     |
| Wait Whisker | Nicki Minaj     |
| Linnie Ponnsett | Nicki Minaj     |
| Cos Northern | Nicki Minaj     |
| Murry Benion | Nicki Minaj     |
| Sadye Ellcome | Nicki Minaj     |
| Hanan Headrick | Nicki Minaj     |
| Elroy Aysh   | Nicki Minaj     |
| Valentina Westell | Nicki Minaj     |
| Dannie de Villier | Nicki Minaj     |
| Sylvia Giacopetti | Nicki Minaj     |
| Nady Tennewell | Nicki Minaj     |
| Jacquelin Burnand | Coldplay        |
| Tedd Eaglen  | Coldplay        |
| Leslie Myott | Coldplay        |
| Averill Ehrat | Coldplay        |
| Lynn Meckiff | Coldplay        |
| Clyve Beagin | Maroon 5        |
| Tedd Eaglen  | Maroon 5        |
| Doll Greenley | Maroon 5        |
| Aindrea De Cruce | Maroon 5        |
| Bradly MacGill | Maroon 5        |
| Bary Halfacree | Maroon 5        |
| Avrit Deerness | Maroon 5        |
| Auria Simeoni | Maroon 5        |
| Ker Quick    | Maroon 5        |
| Jethro Cheston | Maroon 5        |
| Britta Etty  | Maroon 5        |
| Alberta McGruar | Maroon 5        |
| Klemens Stones | Maroon 5        |
| Flore Island | Maroon 5        |
| Adriena Bloan | Maroon 5        |
| Lorenza Hollyland | Maroon 5        |
| Hilario Forsythe | Maroon 5        |
| Sammy Brendel | Maroon 5        |
| Cosetta Haggith | Maroon 5        |
| Francis Revie | Maroon 5        |
| Gavin Cuttler | Maroon 5        |
| Conant Hallett | Imagine Dragons |
| Honoria Gippes | Imagine Dragons |
| Bary Halfacree | Imagine Dragons |
| Susette Armstead | Imagine Dragons |
| Alanah Jaume | Imagine Dragons |
| Felecia Borless | Imagine Dragons |
| Cleveland Jessup | Imagine Dragons |
| Gavin Cuttler | Imagine Dragons |
| Tyrus Manuel | Imagine Dragons |
| Tabby Muress | Imagine Dragons |
| Aldric Roycroft | Imagine Dragons |
| Kipp Chree   | Imagine Dragons |
| Pennie Piddington | Sam Smith       |
| Ermanno Raulston | Sam Smith       |
| Raul Mendes  | Sam Smith       |
| Klemens Stones | Sam Smith       |
| Shaylah Begbie | Sam Smith       |
| Mariya Carlett | Sia             |
| Drew Sircombe | Sia             |
| Stella Tills | Sia             |
| Flore Island | Sia             |
| Catharine Hele | Sia             |
| Ernesto Rusling | Sia             |
| Jeff Evett   | Sia             |
| Carrissa Aris | Sia             |
| Marilin Steet | Sia             |
| Hoebart Loving | Sia             |
| Darleen Lingfoot | Sia             |
| Lowe Traynor | Sia             |
| Roger Hindenberger | Sia             |
| Barry Goodge | Sia             |
| Ardath Twentyman | Sia             |
| Danette Massei | Sia             |
| Monah Bachmann | Sia             |
| Burr Dunckley | Sia             |
| Luella Ivasechko | Sia             |
| Arabelle Curness | Sia             |
| Phelia Churchward | Sia             |
| Drugi Mattiussi | Lorde           |
| Fabio Bottom | Lorde           |
| Sada Edes    | Lorde           |
| Ker Quick    | Lorde           |
| Barry Goodge | Lorde           |
| Brittaney De Maine | Lorde           |
| Carin Castletine | Lorde           |
| Paul Riehm   | Lorde           |
| Monah Bachmann | Lorde           |
| Augustin Triplet | Lorde           |
| Cyndi Collins | Lorde           |
| Cleo Peirpoint | Lorde           |
| Alexandro Yushachkov | Lorde           |
| Bary Halfacree | Lorde           |
| Marcelle Hancock | Lorde           |
| Luella Ivasechko | Lorde           |
| Blaire Rosander | Lorde           |
| Mac Figin    | Lorde           |
| Adaline Louthe | Lorde           |
| Arlen Bondy  | Lorde           |
| Noel Kubiak  | Lorde           |
| Mahala McArley | Miley Cyrus     |
| Tiebold Gorges | Miley Cyrus     |
| Manolo Trytsman | Miley Cyrus     |
| Jaye Trosdall | John Legend     |
| Gracia Binder | John Legend     |
| Gaston Gehring | John Legend     |
| Darleen Lingfoot | Dua Lipa        |
| Debor Pietesch | Dua Lipa        |
| Darius Veldman | Dua Lipa        |
| Nonnah Morrish | Dua Lipa        |
| Helen Garoghan | Dua Lipa        |
| Pippo Bolliver | Dua Lipa        |
| Nikolai Williment | Dua Lipa        |
| Otes Cowp    | Dua Lipa        |
| Davy Rollitt | Dua Lipa        |
| Roanne Orridge | Dua Lipa        |
| Anjanette McLeary | Calvin Harris   |
| Isaiah Thresher | Calvin Harris   |
| Dyna McAndrew | Calvin Harris   |
| Alane Shelp  | Calvin Harris   |
| Mil McInnery | Calvin Harris   |
| Nowell Olivia | Calvin Harris   |
| Maurise Wrathmall | Calvin Harris   |
| Tallulah Hegg | Selena Gomez    |
| Kris Mingay  | Selena Gomez    |
| Dallas Tidbald | Selena Gomez    |
| Leslie Myott | Selena Gomez    |
| April Filipyev | Selena Gomez    |
| Gratia Simm  | Selena Gomez    |
| Carena Mounsey | Selena Gomez    |
| Claire Oliveto | Selena Gomez    |
| Isaiah Thresher | Selena Gomez    |
| Saul Lindenberg | Selena Gomez    |
| Whitby Hoffmann | Camila Cabello  |
| Christean O'Riordan | Camila Cabello  |
| Lenka Travers | Camila Cabello  |
| Lenard Call  | Camila Cabello  |
| Gerhardt Keaves | Camila Cabello  |
| Xerxes Weedall | Camila Cabello  |
| Finlay Douberday | Camila Cabello  |
| Pooh Prine   | Camila Cabello  |
| Torrin Spofford | Camila Cabello  |
| Yul Pietzker | Camila Cabello  |
| Delilah De L'Isle | Camila Cabello  |
| Bordie Buzzing | Camila Cabello  |
| Rodney Sibthorp | Camila Cabello  |
| Brendin Zavattieri | Camila Cabello  |
| Binnie Gomme | Camila Cabello  |
| Kessiah Noke | Camila Cabello  |
| Hi Wyllcock  | Camila Cabello  |
| Nissy Mustin | Camila Cabello  |
| Lowe Traynor | Camila Cabello  |
| Hi Wyllcock  | Camila Cabello  |
| Lesya Haack  | Post Malone     |
| Blaire Rosander | Post Malone     |
| Baldwin Eyrl | Post Malone     |
| Thaine Thing | Post Malone     |
| Frasier Brister | Post Malone     |
| Karie Shimmans | Post Malone     |
| Tera Easom   | Post Malone     |
| Joelynn Tilby | Post Malone     |
| Allyn Dewey  | Cardi B         |
| Hanan Headrick | Cardi B         |
| Beatrice Snel | Cardi B         |
| Gill Audley  | Cardi B         |
| Lynde Petran | Cardi B         |
| Sarene Josebury | Cardi B         |
| Catharine Hele | Cardi B         |
| Vale Yakov   | Cardi B         |
| Layne Lofts  | Cardi B         |
| Beale Abatelli | Cardi B         |
| Rheta Daw    | Cardi B         |
| Catharine Hele | Cardi B         |
| Jodie O'Dreain | Cardi B         |
| Adriena Bloan | Jason Derulo    |
| Joellyn Lamplough | Jason Derulo    |
| Bard Cockett | Jason Derulo    |
| Auria Simeoni | Jason Derulo    |
| Rosalie Durston | Jason Derulo    |
| Coralie Beric | Jason Derulo    |
| Sylvia Giacopetti | Jason Derulo    |
| Haskell Delort | Jason Derulo    |
| Mac Figin    | Jason Derulo    |
| Percy Younger | Jason Derulo    |
| Gaston Gehring | Jason Derulo    |
| Mirabella Fritchley | Jason Derulo    |
| Marisa Halwell | Jason Derulo    |
| Gavin Cuttler | Jason Derulo    |
| Zollie Currin | Jason Derulo    |
| Filmore Crolla | Jason Derulo    |
| Tabby Muress | Jason Derulo    |
| Reggi McLardie | Jason Derulo    |
| Wait Whisker | Jason Derulo    |
| Quinn Oliphand | Jason Derulo    |
| Anabel Pywell | Halsey          |
| Jilly Skudder | Halsey          |
| Kacey Grayson | Halsey          |
| Salvatore Casarili | Halsey          |
| Wells Dyment | Halsey          |
| Mirabella Fritchley | Halsey          |
| Nonnah Morrish | Halsey          |
| Nari Emerine | Halsey          |
| Timofei Von Der Empten | Halsey          |
| Shari Narracott | Halsey          |
| Raul Mendes  | Halsey          |
| Zollie Currin | Halsey          |
| Ervin Von Brook | Halsey          |
| Phillipp Clementucci | Halsey          |
| Adaline Louthe | Halsey          |
| Cherise Rubinlicht | Halsey          |
| Nola Lehrmann | Halsey          |
| Betsy Sherel | Halsey          |
| Darius Veldman | Halsey          |
| Stella Tills | Halsey          |
| Hi Wyllcock  | Halsey          |
| Grace Dealey | Halsey          |
| Ernesto Rusling | Halsey          |
| Flynn Giacomi | Halsey          |
| Lexi Mallinar | Halsey          |
| Claiborne Comar | Halsey          |
| Chev Kepe    | Halsey          |
| Danette Massei | Charlie Puth    |
| Adelbert Hawney | Charlie Puth    |
| Brittaney De Maine | Charlie Puth    |
| L;urette Izacenko | Charlie Puth    |
| Minny Tungate | Charlie Puth    |
| Murry Benion | Charlie Puth    |
| Joanie Abbots | Charlie Puth    |
| Milton Arkow | Charlie Puth    |
| Lynn Meckiff | Charlie Puth    |
| Jamie Slaght | Charlie Puth    |
| Carena Mounsey | Charlie Puth    |
| Rozalie le Keux | Charlie Puth    |
| Isaiah Thresher | Charlie Puth    |
| Bary Halfacree | Charlie Puth    |
| Vallie Faldo | Charlie Puth    |
| Sacha Bunce  | Charlie Puth    |
| Rebekkah Bignal | Marshmello      |
| Marcie Wenger | Marshmello      |
| Nari Emerine | Marshmello      |
| Bary Halfacree | Marshmello      |
| Christean O'Riordan | Marshmello      |
| Poppy Pendlebery | Marshmello      |
| Mia Chellenham | The Chainsmokers |
| Sylvia Giacopetti | The Chainsmokers |
| Averill Ehrat | The Chainsmokers |
| Antonie Tregonna | The Chainsmokers |
| Lorettalorna Cominetti | The Chainsmokers |
| Amandi Mellon | P!nk            |
| Eugene Cage  | P!nk            |
| Shari Narracott | P!nk            |
| Roana Zavattieri | P!nk            |
| Fraze Dowling | P!nk            |
| Vale Yakov   | P!nk            |
| Katerine Dullaghan | P!nk            |
| Phyllida Peare | P!nk            |
| Chester Pencot | P!nk            |
| Quinn Oliphand | P!nk            |
| Cos Northern | P!nk            |
| Magdalene Chapell | Lana Del Rey    |
| Maurise Wrathmall | Lana Del Rey    |
| Jeff Evett   | Eminem          |
| Merilyn Macieiczyk | Eminem          |
| Beatrice Snel | Eminem          |
| Jacquelin Burnand | Eminem          |
| Benjamen Maundrell | Eminem          |
| Flory Braybrooks | Eminem          |
| Manolo Trytsman | Eminem          |
| Noel Kubiak  | Eminem          |
| Shanan Hardes | Eminem          |
| Xerxes Weedall | Eminem          |
| Whit Hambleton | Eminem          |
| Caresa O' Mullan | Eminem          |
| Rozalie le Keux | Eminem          |
| Wilt Atyea   | Eminem          |
| Drugi Mattiussi | Shakira         |
| Gracia Binder | Shakira         |
| Rozalie le Keux | Shakira         |
| Elroy Aysh   | Pitbull         |
| Willamina Munkley | Pitbull         |
| Erasmus Stretton | Pitbull         |
| Marillin Winkless | Pitbull         |
| Nate Creavan | Pitbull         |
| Pennie Piddington | Pitbull         |
| Herbie Burgwyn | Pitbull         |
| Damiano Duckers | Pitbull         |
| Selestina Reisen | Pitbull         |
| Leonelle Schlagtmans | Pitbull         |
| Flynn Giacomi | Pitbull         |
| Rania Causby | Pitbull         |
| Nelli Corrison | Pitbull         |
| Even Battle  | Pitbull         |
| Ronni Quodling | Pitbull         |
| Eugene Cage  | Jennifer Lopez  |
| Winthrop Casillis | Jennifer Lopez  |
| Dallas Tidbald | Jennifer Lopez  |
| Claire Oliveto | Jennifer Lopez  |
| Jeremy O'Callaghan | Jennifer Lopez  |
| Mirabella Fritchley | Jennifer Lopez  |
| Beale Abatelli | Jennifer Lopez  |
| Mureil Ropars | Jennifer Lopez  |
| Magdalene Chapell | Jennifer Lopez  |
| Ervin Von Brook | Jennifer Lopez  |
| Isaiah Thresher | Jennifer Lopez  |
| Dyna McAndrew | Jennifer Lopez  |
| Saul Lindenberg | Jennifer Lopez  |
| Sandy Durn   | Jennifer Lopez  |
| Agnes Lambertazzi | Jennifer Lopez  |
| Arabelle Curness | Jennifer Lopez  |
| Clerkclaude Eisig | Jennifer Lopez  |
| Amandi Mellon | Jennifer Lopez  |
| Caresa O' Mullan | Jennifer Lopez  |
| Luella Ivasechko | Jennifer Lopez  |
| Elie Goad    | Jennifer Lopez  |
| Chester Pencot | Jennifer Lopez  |
| Cristiano Forsard | Jennifer Lopez  |
| Legra Hallitt | Jennifer Lopez  |
| Monti Chisman | Jennifer Lopez  |
| Sibby O'Mullally | Jennifer Lopez  |
| Erasmus Stretton | Usher           |
| Marrilee Juzek | Usher           |
| Salvatore Casarili | Usher           |
| Bernard Donavan | Usher           |
| Maria Ruck   | Usher           |
| Morganica Cesaric | Usher           |
| Elicia Bonifant | Usher           |
| Nari Emerine | Usher           |
| Efrem Currie | Usher           |
| Stanislaw Ibbetson | Usher           |
| Selestina Reisen | Usher           |
| Jodie O'Dreain | Usher           |
| Gratia Simm  | Avril Lavigne   |
| Neila Perch  | Avril Lavigne   |
| Joellyn Lamplough | Avril Lavigne   |
| Ermanno Raulston | Avril Lavigne   |
| Yvonne Braine | Avril Lavigne   |
| Rodney Sibthorp | Avril Lavigne   |
| Stanislaw Ibbetson | Avril Lavigne   |
| Silvanus Struan | Avril Lavigne   |
| Britta Etty  | Avril Lavigne   |
| Estrellita Vasin | Avril Lavigne   |
| Francis Revie | Avril Lavigne   |
| Gavrielle Pumfrey | Avril Lavigne   |
| Carena Mounsey | Avril Lavigne   |
| Carena Mounsey | Avril Lavigne   |
| Willie Chenery | Avril Lavigne   |
| Coralie Beric | Avril Lavigne   |
| Smitty Maudling | Avril Lavigne   |
| Elicia Bonifant | Alicia Keys     |
| Bernardina Gricewood | Alicia Keys     |
| Linn Penbarthy | Alicia Keys     |
| Bone Lackham | Alicia Keys     |
| Zollie Currin | Alicia Keys     |
| Janeen Rudolph | Alicia Keys     |
| Hillier Dradey | Alicia Keys     |
| Percy Younger | Alicia Keys     |
| Norrie Rehme | Alicia Keys     |
| Brittaney De Maine | Alicia Keys     |
| Berke Oaker  | Britney Spears  |
| Britta Etty  | Britney Spears  |
| April Filipyev | Britney Spears  |
| Marilin Steet | Britney Spears  |
| Katerine Dullaghan | Britney Spears  |
| Lynde Petran | Britney Spears  |
| Percy Younger | Britney Spears  |
| Edwin Bakes  | Britney Spears  |
| Nissy Mustin | Christina Aguilera |
| Bary Halfacree | Christina Aguilera |
| Sarene Josebury | Christina Aguilera |
| Kermy Norrington | Christina Aguilera |
| Toinette Keirle | Christina Aguilera |
| Christean O'Riordan | Kelly Clarkson  |
| Cy Slaten    | Kelly Clarkson  |
| Anjanette McLeary | Kelly Clarkson  |
| Wait Whisker | Kelly Clarkson  |
| Even Battle  | Kelly Clarkson  |
| Efrem Currie | Kelly Clarkson  |
| Raul Gillyett | Kelly Clarkson  |
| Tabby Muress | Kelly Clarkson  |
| Stanislaw Ibbetson | Kelly Clarkson  |
| Bernardine Featherby | Kelly Clarkson  |
| Sandy Durn   | Gwen Stefani    |
| Otes Cowp    | Gwen Stefani    |
| Finlay Douberday | Gwen Stefani    |
| Edwin Bakes  | Gwen Stefani    |
| Mair Trever  | Gwen Stefani    |
| Berke Oaker  | Gwen Stefani    |
| Sada Edes    | Gwen Stefani    |
| Caspar Shave | Gwen Stefani    |
| Betsy Sherel | Gwen Stefani    |
| Beltran Myles | Gwen Stefani    |
| Carena Mounsey | Gwen Stefani    |
| Sandy Durn   | Gwen Stefani    |
| Salvatore Casarili | Gwen Stefani    |
| Karlik Barrat | Gwen Stefani    |
| Juli Machent | Gwen Stefani    |
| Smitty Maudling | Gwen Stefani    |
| Jacquelin Burnand | Gwen Stefani    |
| Gae Vogt     | Gwen Stefani    |
| Helen Garoghan | Gwen Stefani    |
| Lowe Traynor | Gwen Stefani    |
| Garth Barabisch | Gwen Stefani    |
| Valli Smither | Gwen Stefani    |
| Tessie Dufall | Justin Timberlake |
| Berte Brahm  | Justin Timberlake |
| Lavinie Hardwidge | Justin Timberlake |
| Eddie Papis  | Justin Timberlake |
| Udale Myall  | Lil Nas X       |
| Adriena Bloan | Lil Nas X       |
| Norrie Rehme | Lil Nas X       |
| Ermanno Raulston | Lil Nas X       |
| Claire Oliveto | Lil Nas X       |
| Bradly Helis | Lil Nas X       |
| Erhart Broker | Lil Nas X       |
| Grace Dealey | Lil Nas X       |
| Evaleen Dofty | Lil Nas X       |
| Michell Back | Lil Nas X       |
| Georgena Reeveley | Lil Nas X       |
| Willie Chenery | Lil Nas X       |
| Griswold Meus | Lil Nas X       |
| Tannie Pantridge | Lil Nas X       |
| Cos Northern | Lil Nas X       |
| Bradly MacGill | Lil Nas X       |
| Gavin Cuttler | Lil Nas X       |
| Kacey Grayson | Meghan Trainor  |
| Laetitia Marnes | Meghan Trainor  |
| Vallie Faldo | Meghan Trainor  |
| Lenka Travers | Meghan Trainor  |
| Huntley Androli | Meghan Trainor  |
| Janeen Rudolph | Demi Lovato     |
| Hoebart Loving | Demi Lovato     |
| Karie Shimmans | Demi Lovato     |
| Lorrin Karlolczak | Demi Lovato     |
| Catharine Hele | Demi Lovato     |
| Gaston Gehring | Demi Lovato     |
| Elroy Aysh   | Demi Lovato     |
| Dannie de Villier | One Direction   |
| Yvonne Braine | One Direction   |
| Gavin Cuttler | One Direction   |
| Rey Hammersley | One Direction   |
| Zollie Valerius | One Direction   |
| Nonnah Morrish | One Direction   |
| Tallulah Hegg | One Direction   |
| Willamina Munkley | One Direction   |
| Cos Northern | One Direction   |
| Vale Yakov   | One Direction   |
| Rheta Daw    | One Direction   |
| Hartwell Goricke | One Direction   |
| Penny Stadden | One Direction   |
| Caresa O' Mullan | One Direction   |
| Michell Back | One Direction   |
| Isaiah Thresher | One Direction   |
| Ramona Faircliffe | One Direction   |
| Rodney Sibthorp | One Direction   |
| Mirabella Fritchley | One Direction   |
| Lorna Fatharly | Backstreet Boys |
| Betta Pevreal | Backstreet Boys |
| Sarene Josebury | Backstreet Boys |
| Clementina Lemmertz | Backstreet Boys |
| Lorrin Karlolczak | Backstreet Boys |
| Bary Halfacree | Backstreet Boys |
| Leonhard Tant | Backstreet Boys |
| Cyndi Collins | Backstreet Boys |
| Sandy Mordacai | NSYNC           |
| Murry Benion | NSYNC           |
| Bary Halfacree | NSYNC           |
| Damiano Duckers | NSYNC           |
| Odey Blackburne | NSYNC           |
| Magdalene Chapell | NSYNC           |
| Danyelle Steuart | NSYNC           |
| Ollie Twining | NSYNC           |
| Glenna Ference | Destiny's Child |
| Denny Greening | Destiny's Child |
| Stella Tills | Destiny's Child |
| Delilah De L'Isle | Destiny's Child |
| Arlen Maharey | Destiny's Child |
| Claiborne Comar | Destiny's Child |
| Thurstan Billingham | Destiny's Child |
| Tobit Igounet | Destiny's Child |
| Wyndham Dillon | Spice Girls     |
| Arlen Maharey | Spice Girls     |
| Salvatore Casarili | Spice Girls     |
| Helen Garoghan | Spice Girls     |
| Linn Penbarthy | Spice Girls     |
| Zola Sawley  | Spice Girls     |
| Nicola Stratten | Spice Girls     |
| Karie Shimmans | Spice Girls     |
| Maurise Wrathmall | Spice Girls     |
| Katerine Dullaghan | Spice Girls     |
| Wilt Atyea   | Spice Girls     |
| Shaun Vickery | Spice Girls     |
| Dante Simmans | Spice Girls     |
| Monah Bachmann | Spice Girls     |
| Rasia MacKeeg | Spice Girls     |
| Christean O'Riordan | Spice Girls     |
| Albert Ortsmann | Spice Girls     |
| Carrissa Aris | Spice Girls     |
| Marcie Wenger | The Beatles     |
| Goldarina Nicolson | The Beatles     |
| Phelia Churchward | The Beatles     |
| Delilah De L'Isle | Queen           |
| Roxine Mooney | Queen           |
| Gracia Binder | Queen           |
| Fabio Bottom | Queen           |
| Amargo Knutsen | Queen           |
| Milton Arkow | Queen           |
| Damiano Duckers | Michael Jackson |
| Vallie Faldo | Michael Jackson |
| Caspar Shave | Michael Jackson |
| Cristiano Forsard | Michael Jackson |
| Nonnah Morrish | Michael Jackson |
| Drugi Mattiussi | Elton John      |
| Reggi McLardie | Elton John      |
| Blaire Rosander | Elton John      |
| Cleveland Jessup | Elton John      |
| Clementina Lemmertz | Elton John      |
| Carena Mounsey | Elton John      |
| Maria Ruck   | Elton John      |
| Karie Shimmans | Elton John      |
| Shaylah Begbie | Elton John      |
| Maurise Wrathmall | Elton John      |
| Benedikt Van Der Vlies | Madonna         |
| Madeline Agott | Madonna         |
| Rebekkah Bignal | Madonna         |
| Alanah Jaume | Madonna         |
| Zollie Valerius | Madonna         |
| Fraze Dowling | Madonna         |
| Prudi Jales  | Whitney Houston |
| Albert Ortsmann | Whitney Houston |
| Mia Chellenham | Whitney Houston |
| Juli Machent | Whitney Houston |
| Alie O'Calleran | Whitney Houston |
| Jamie Slaght | Whitney Houston |
| Stacie Westman | Whitney Houston |
| Nathan Newberry | Whitney Houston |
| Herbie Burgwyn | Prince          |
| Flore Storck | Prince          |
| Janet Broker | Prince          |
| Marisa Halwell | Prince          |
| Roanne Orridge | Prince          |
| Agnes Lambertazzi | Prince          |
| Antone Fripps | Prince          |
| Eirena Middler | Prince          |
| Carena Mounsey | Prince          |
| Benjamen Maundrell | Prince          |
| Rasia MacKeeg | Prince          |
| Burr Dunckley | Prince          |
| Ervin Von Brook | Prince          |
| Murry Benion | Prince          |
| April Filipyev | Prince          |
| Garth Barabisch | Prince          |
| Efren Sutherns | Prince          |
| Nowell Olivia | Prince          |
| Simmonds Segges | Prince          |
| Phyllida Peare | Bob Dylan       |
| Ginnifer Mulkerrins | Bob Dylan       |
| Pietrek Simounet | Bob Dylan       |
| Sylvia Giacopetti | Bob Dylan       |
| Thaine Thing | David Bowie     |
| Nola Lehrmann | David Bowie     |
| Nevil Mahomet | David Bowie     |
| Pebrook Vittet | David Bowie     |
| Fabio Bottom | David Bowie     |
| Jobye Emett  | David Bowie     |
| Laetitia Marnes | David Bowie     |
| Tyrus Manuel | David Bowie     |
| Burr Dunckley | David Bowie     |
| Tabby Muress | David Bowie     |
| Benedikt Van Der Vlies | Stevie Wonder   |
| Gill Audley  | Stevie Wonder   |
| Misha Canfer | Stevie Wonder   |
| Madeline Agott | Stevie Wonder   |
| Eugene Cage  | Stevie Wonder   |
| Hanan Headrick | Janet Jackson   |
| Roana Zavattieri | Janet Jackson   |
| Zollie Currin | Janet Jackson   |
| Layne Lofts  | Janet Jackson   |
| Whit Hambleton | Janet Jackson   |
| Scotti Crowche | Janet Jackson   |
| Neila Perch  | Tina Turner     |
| Suzanna Vitet | Tina Turner     |
| Drew Sircombe | Tina Turner     |
| Pietrek Simounet | Tina Turner     |
| Stella Tills | Tina Turner     |
| Misha Canfer | Tina Turner     |
| Scotti Crowche | Tina Turner     |
| Averill Ehrat | Tina Turner     |
| Marcelle Hancock | Tina Turner     |
| Rhiamon Grigolli | Tina Turner     |
| Rhiamon Ceccoli | Tina Turner     |
| Tabatha Berringer | Tina Turner     |
| Tera Easom   | Tina Turner     |
| Efrem Currie | Cher            |
| Finlay Douberday | Cher            |
| Arlen Bondy  | Cher            |
| Sibby O'Mullally | Cher            |
| Adelbert Hawney | Cher            |
| Aindrea De Cruce | Cher            |
| Melitta Prujean | Cher            |
| Darius Veldman | Cher            |
| Alistair Timmens | Barbra Streisand |
| Wells Dyment | Barbra Streisand |
| Stella Tills | Barbra Streisand |
| Siffre Tattam | Frank Sinatra   |
| Percy Younger | Frank Sinatra   |
| Monah Bachmann | Frank Sinatra   |
| Rheta Benes  | Frank Sinatra   |
| Harlene Longfoot | Frank Sinatra   |
| Dante Simmans | Frank Sinatra   |
| Flory Braybrooks | Frank Sinatra   |
| Sarene Josebury | Frank Sinatra   |
| Kermy Norrington | Frank Sinatra   |
| Estrellita Vasin | Frank Sinatra   |
| Murry Benion | Frank Sinatra   |
| Stacie Westman | Frank Sinatra   |
| Christean O'Riordan | Frank Sinatra   |
| Bernard Donavan | Frank Sinatra   |
| Davy Rollitt | Elvis Presley   |
| Nomi Mattaus | Elvis Presley   |
| Leslie Myott | Elvis Presley   |
| Moise Jebb   | Elvis Presley   |
| Augustin Holbarrow | Johnny Cash     |
| Gae Vogt     | Johnny Cash     |
| Lorenza Hollyland | Johnny Cash     |
| Drugi Mattiussi | Johnny Cash     |
| Britta Etty  | Johnny Cash     |
| Fidel Hukins | Johnny Cash     |
| Fraze Dowling | Johnny Cash     |
| Adriena Bloan | Johnny Cash     |
| Gaston Gehring | Johnny Cash     |
| Whitby Hoffmann | Willie Nelson   |
| Tyrus Manuel | Willie Nelson   |
| Mureil Ropars | Willie Nelson   |
| Glenna Ference | Willie Nelson   |
| Hartwell Goricke | Willie Nelson   |
| Eddie Papis  | Willie Nelson   |
| Bernardina Gricewood | Kenny Rogers    |
| Suzanna Vitet | Kenny Rogers    |
| Estrellita Vasin | Kenny Rogers    |
| Alexandro Yushachkov | Kenny Rogers    |
| Bone Lackham | Kenny Rogers    |
| Orelie Trinbey | Merle Haggard   |
| Phyllida Peare | Merle Haggard   |
| Flore Storck | Merle Haggard   |
| Lorna Fatharly | Merle Haggard   |
| Ker Quick    | Merle Haggard   |
| Marrilee Klauer | Merle Haggard   |
| Darleen Lingfoot | George Strait   |
| Yvonne Braine | George Strait   |
| Nola Lehrmann | George Strait   |
| Denny Greening | George Strait   |
| Damiano Duckers | George Strait   |
| Sharla Taberer | George Strait   |
| Dania Budget | George Strait   |
| Adiana Cockayme | George Strait   |
| Minny Tungate | George Strait   |
| Lorna Fatharly | Garth Brooks    |
| Xavier Saladino | Garth Brooks    |
| Roanne Orridge | Garth Brooks    |
| Kacey Grayson | Garth Brooks    |
| Ervin Von Brook | Garth Brooks    |
| Sadye Ellcome | Garth Brooks    |
| Coralie Beric | Garth Brooks    |
| Lorenza Hollyland | Shania Twain    |
| Phyllida Peare | Shania Twain    |
| Valentina Westell | Shania Twain    |
| Baldwin Eyrl | Shania Twain    |
| Bary Halfacree | Shania Twain    |
| Avrit Deerness | Shania Twain    |
| Juli Machent | Shania Twain    |
| Ker Quick    | Shania Twain    |
| Agnola Shepstone | Shania Twain    |
| Damiano Duckers | Shania Twain    |
| Clari Gymblett | Shania Twain    |
| Lauritz Oughtright | Shania Twain    |
| Tobit Igounet | Shania Twain    |
| Noel Kubiak  | Shania Twain    |
| Darleen Lingfoot | Shania Twain    |
| Winthrop Casillis | Shania Twain    |
| Dannie de Villier | Shania Twain    |
| Amargo Knutsen | Shania Twain    |
| Antone Fripps | Shania Twain    |
| Carlynn Worstall | Shania Twain    |
| Cherise Rubinlicht | Carrie Underwood |
| Alane Shelp  | Carrie Underwood |
| Leonhard Tant | Blake Shelton   |
| Toinette Keirle | Blake Shelton   |
| Adiana Cockayme | Blake Shelton   |
| Filmore Crolla | Blake Shelton   |
| Murry Benion | Blake Shelton   |
| Jaymee Costley | Blake Shelton   |
| Ermanno Raulston | Blake Shelton   |
| Rey Hammersley | Blake Shelton   |
| Edwin Bakes  | Blake Shelton   |
| Bernardine Featherby | Blake Shelton   |
| Estele Stoyle | Blake Shelton   |
| Cy Slaten    | Luke Bryan      |
| Doll Greenley | Luke Bryan      |
| Reggi McLardie | Luke Bryan      |
| Averill Ehrat | Luke Bryan      |
| Berte Brahm  | Luke Bryan      |
| Marrilee Juzek | Jason Aldean    |
| Sibby O'Mullally | Jason Aldean    |
| Pennie Piddington | Jason Aldean    |
| April Filipyev | Jason Aldean    |
| Claybourne Bedward | Jason Aldean    |
| Simmonds Segges | Jason Aldean    |
| Christean O'Riordan | Keith Urban     |
| Marcie Wenger | Keith Urban     |
| Nicola Stratten | Keith Urban     |
| Marrilee Klauer | Keith Urban     |
| Shaun Vickery | Keith Urban     |
| Bernardine Featherby | Keith Urban     |
| Mariya Carlett | Keith Urban     |
| Merrel Barbey | Keith Urban     |
| Belicia Lillicrop | Keith Urban     |
| Cos Northern | Keith Urban     |
| Norrie Rehme | Tim McGraw      |
| Finlay Douberday | Tim McGraw      |
| Anjanette McLeary | Tim McGraw      |
| Xerxes Weedall | Tim McGraw      |
| Frankie Midlar | Tim McGraw      |
| Darleen Lingfoot | Tim McGraw      |
| Otes Cowp    | Tim McGraw      |
| Vicki Portugal | Tim McGraw      |
| Tabby Muress | Tim McGraw      |
| Lenard Call  | Tim McGraw      |
| Rosalie Durston | Tim McGraw      |
| Herbie Burgwyn | Tim McGraw      |
| Gaston Gehring | Tim McGraw      |
| Isaiah Thresher | Tim McGraw      |
| Marisa Halwell | Tim McGraw      |
| Honoria Gippes | Tim McGraw      |
| Shari Narracott | Tim McGraw      |
| Bone Lackham | Tim McGraw      |
| Nikolia Tenpenny | Tim McGraw      |
| Nikolai Williment | Tim McGraw      |
| Christean O'Riordan | Faith Hill      |
| Jaye Trosdall | Faith Hill      |
| Cosetta Haggith | Faith Hill      |
| Reggi McLardie | Faith Hill      |
| Sarene Josebury | Faith Hill      |
| Adelbert Hawney | Faith Hill      |
| Aindrea De Cruce | Faith Hill      |
| Trumann Wiffler | Faith Hill      |
| Fitzgerald Hefferan | Faith Hill      |
| Helen Garoghan | Faith Hill      |
| Rheta Daw    | Faith Hill      |
| Lavinie Hardwidge | Faith Hill      |
| Lorrin Karlolczak | Faith Hill      |
| Madeline Agott | Faith Hill      |
| Suzanna Vitet | Faith Hill      |
| Shari Narracott | Faith Hill      |
| Whit Hambleton | Faith Hill      |
| Hanan Headrick | Faith Hill      |
| Carlynn Worstall | Faith Hill      |
| Wyndham Dillon | Miranda Lambert |
| Catharine Hele | Miranda Lambert |
| Kinsley Swarbrick | Miranda Lambert |
| Timofei Von Der Empten | Miranda Lambert |
| Sidonia Witul | Miranda Lambert |
| Thurstan Billingham | Miranda Lambert |
| Rosalie Durston | Miranda Lambert |
| Carena Mounsey | Miranda Lambert |
| Augustin Holbarrow | Miranda Lambert |
| Delilah De L'Isle | Miranda Lambert |
| Jeremy O'Callaghan | Miranda Lambert |
| Saul Lindenberg | Miranda Lambert |
| Mureil Ropars | Miranda Lambert |
| Binnie Gomme | Miranda Lambert |
| Alessandra Cheshir | Miranda Lambert |
| Efren Sutherns | Miranda Lambert |
| Salvatore Casarili | Zac Brown Band  |
| Dannie de Villier | Zac Brown Band  |
| Luella Ivasechko | Zac Brown Band  |
| Valentina Westell | Zac Brown Band  |
| Goldarina Nicolson | Zac Brown Band  |
| Raul Mendes  | Zac Brown Band  |
| Lorrin Karlolczak | Zac Brown Band  |
| Sadye Pancoast | Zac Brown Band  |
| Warren Cammomile | Zac Brown Band  |
| Shalna Ateridge | Zac Brown Band  |
| Wyndham Dillon | Zac Brown Band  |
| Nola Lehrmann | Zac Brown Band  |
| Goldarina Nicolson | Zac Brown Band  |
| Torrin Spofford | Zac Brown Band  |
| Shaun Vickery | Zac Brown Band  |
| Maurise Wrathmall | Zac Brown Band  |
| Jaye Trosdall | Lady A          |
| Roger Hindenberger | Lady A          |
| Wayne Cogzell | Lady A          |
| Tobit Igounet | Lady A          |
| Simmonds Segges | Lady A          |
| Trumann Wiffler | Lady A          |
| Misha Canfer | Lady A          |
| Vallie Faldo | Lady A          |
| Antonie Tregonna | Lady A          |
| Agnola Shepstone | Lady A          |
| Christean O'Riordan | Lady A          |
| Berke Bronot | Lady A          |
| Worthington Demeza | Lady A          |
| Barbara-anne Gleave | Lady A          |
| Klemens Stones | Lady A          |
| Jobye Emett  | Lady A          |
| Filmore Crolla | Little Big Town |
| Clyve Beagin | Little Big Town |
| Arlen Maharey | Little Big Town |
| Joelynn Tilby | Little Big Town |
| Moise Jebb   | Little Big Town |
+ ------------ + --------------- +
892 rows
```

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
Lists each artist's name, ID, and most-awarded album.

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


Query 4
Lists the ID and name of each venue and orders them by the number of concerts held at the venue. The most popular venues with the most concerts are listed first, while venues with the least number of concerts are listed last.
SELECT Venue.venueID, Venue.venueName, Venue.city, COUNT(*) AS "Number of Concerts"
FROM Concert
JOIN Venue ON venueID = venueID
GROUP BY venueID, venueName, city
ORDER BY COUNT(*) DESC;

This query is useful for artists to use when planning concerts. They may want to look for venues in cities that they are personally unfamiliar with and use the most popular venue as a starting point for their research. Venues that have hosted many concerts have likely gained their status for a reason, and they may be more suitable than other venues for concerts.


Query 5
Lists artists who have released at least 3 albums.
SELECT Artist.artistID, artistName,
 COUNT(albumID) AS "Album count"
FROM Artist
JOIN Album ON Artist.artistID = Album.artistID
GROUP BY Artist.artistID, artistName
HAVING COUNT(albumID) > 3
ORDER BY COUNT(albumID) DESC;

This query is useful because it highlights experienced and established artists in the industry. A manager could use this information to seek out and invest in artists who have the potential to expand their brand through collaborations with other artists, concerts, and product launches.


Query 6
Returns every venue with its name and the number of employees who work there, including venues with zero employees, sorted from most staffed to least staffed
SELECT Venue.venueID, Venue.venueName, COUNT(Employee.employeeID) AS employee_count
FROM Venue
LEFT JOIN Employee ON Employee.venueID = Venue.venueID
GROUP BY Venue.venueID, Venue.venueName
ORDER BY employee_count DESC;

Provides a quick staffing snapshot per location so managers can identify overstaffed or understaffed venues, allocate or reassign personnel, plan hiring, and prioritize operational support where headcount is low.

Query 7
Find songs with the word "love" in the title and displays the song's ID, the name of the song, the ID of the artist who created it, the artist's name, and the album the song is in.
SELECT
  songID,
  songName,
  Song.artistID,
  artistName
  albumID
FROM Song
JOIN Artist ON Song.artistID = Artist.artistID
WHERE songName REGEXP 'love|Love';

This information is useful because love is a common theme among the most popular songs across multiple genres. A producer may want to find songs that are written about love to study trends in music listeners, or if they are creating promotional material for certain holidays like Valentine's Day.

Query 8
Finds venue employees who supervise more than 3 people. Displays the supervisor's ID, name, and the number of direct reports they have.
SELECT
  sup.employeeID AS supervisorID,
  sup.employeeName AS supervisorName,
  COUNT(sub.employeeID) AS direct_reports
FROM Employee sup
JOIN Employee sub ON sub.supervisorID = sup.employeeID
GROUP BY sup.employeeID, sup.employeeName
HAVING COUNT(sub.employeeID) > 3
ORDER BY direct_reports DESC;

This query is useful for organizational and budgetary insights in the event planning industry. A venue's higher management can look at this data to see which employees may be stretched too thin in their job duties. This data can also be used to streamline accountability among large teams of employees within different divisions.

Query 9
Displays the album ID, album name, artist ID, and artist name of albums that did not receive any awards.
```
Execute:
> SELECT Album.albumID, Album.albumName, Artist.artistID, Artist.artistName
FROM Album
JOIN Artist ON Album.artistID = Artist.artistID
WHERE NOT EXISTS (
  SELECT *
  FROM Award
  WHERE Award.albumID = Album.albumID
)
ORDER BY Artist.artistName, Album.albumName

+ ------------ + -------------- + ------------- + --------------- +
| albumID      | albumName      | artistID      | artistName      |
+ ------------ + -------------- + ------------- + --------------- +
| 222          | Girl on Fire   | 44            | Alicia Keys     |
| 133          | The Blueprint 3 (Jay-Z Album) | 44            | Alicia Keys     |
| 72           | Let Go         | 43            | Avril Lavigne   |
| 232          | Backstreet's Back | 56            | Backstreet Boys |
| 208          | Millennium     | 56            | Backstreet Boys |
| 1            | Guilty         | 73            | Barbra Streisand |
| 186          | The Way We Were (Soundtrack) | 73            | Barbra Streisand |
| 230          | Blake Shelton  | 86            | Blake Shelton   |
| 98           | Single         | 86            | Blake Shelton   |
| 109          | Highway 61 Revisited | 67            | Bob Dylan       |
| 10           | The Freewheelin' Bob Dylan | 67            | Bob Dylan       |
| 147          | The Times They Are a-Changin' | 67            | Bob Dylan       |
| 112          | ...Baby One More Time | 45            | Britney Spears  |
| 160          | Blackout       | 45            | Britney Spears  |
| 83           | In the Zone    | 45            | Britney Spears  |
| 119          | 18 Months      | 25            | Calvin Harris   |
| 88           | Motion         | 25            | Calvin Harris   |
| 25           | Single         | 25            | Calvin Harris   |
| 94           | Shawn Mendes (Deluxe) | 28            | Camila Cabello  |
| 56           | The Hurting. The Healing. The Loving. | 28            | Camila Cabello  |
| 239          | Invasion of Privacy | 30            | Cardi B         |
| 151          | Single         | 30            | Cardi B         |
| 47           | Blown Away     | 85            | Carrie Underwood |
| 43           | Some Hearts    | 85            | Carrie Underwood |
| 145          | Furious 7 (Soundtrack) | 33            | Charlie Puth    |
| 157          | Nine Track Mind | 33            | Charlie Puth    |
| 24           | Voicenotes     | 33            | Charlie Puth    |
| 62           | Heart of Stone | 72            | Cher            |
| 249          | Look at Us (Sonny & Cher Album) | 72            | Cher            |
| 46           | Christina Aguilera | 46            | Christina Aguilera |
| 49           | Stripped       | 46            | Christina Aguilera |
| 118          | Parachutes     | 15            | Coldplay        |
| 166          | Viva La Vida or Death and All His Friends | 15            | Coldplay        |
| 251          | X&Y            | 15            | Coldplay        |
| 152          | David Bowie (Space Oddity) | 68            | David Bowie     |
| 33           | Heroes         | 68            | David Bowie     |
| 130          | Demi           | 54            | Demi Lovato     |
| 4            | Tell Me You Love Me | 54            | Demi Lovato     |
| 172          | Unbroken       | 54            | Demi Lovato     |
| 212          | Survivor       | 58            | Destiny's Child |
| 163          | The Writing's on the Wall | 58            | Destiny's Child |
| 77           | 9 to 5 and Odd Jobs | 77            | Dolly Parton    |
| 27           | Jolene         | 77            | Dolly Parton    |
| 200          | Dua Lipa       | 24            | Dua Lipa        |
| 40           | Honky Chateau  | 63            | Elton John      |
| 110          | Madman Across the Water | 63            | Elton John      |
| 97           | The Lockdown Sessions | 63            | Elton John      |
| 18           | Blue Hawaii (Soundtrack) | 75            | Elvis Presley   |
| 221          | Single         | 75            | Elvis Presley   |
| 243          | Single         | 75            | Elvis Presley   |
| 173          | 8 Mile (Soundtrack) | 38            | Eminem          |
| 244          | Recovery       | 38            | Eminem          |
| 116          | The Marshall Mathers LP | 38            | Eminem          |
| 143          | The Outsiders  | 95            | Eric Church     |
| 177          | Breathe        | 91            | Faith Hill      |
| 241          | Faith          | 91            | Faith Hill      |
| 156          | Take Me as I Am | 91            | Faith Hill      |
| 117          | Dig Your Roots | 96            | Florida Georgia Line |
| 174          | Here's to the Good Times | 96            | Florida Georgia Line |
| 55           | It Might as Well Be Swing | 74            | Frank Sinatra   |
| 74           | My Way         | 74            | Frank Sinatra   |
| 205          | Trilogy: Past, Present & Future | 74            | Frank Sinatra   |
| 215          | In Pieces      | 82            | Garth Brooks    |
| 132          | No Fences      | 82            | Garth Brooks    |
| 127          | Always Never the Same | 81            | George Strait   |
| 51           | Pure Country (Soundtrack) | 81            | George Strait   |
| 203          | Strait from the Heart | 81            | George Strait   |
| 11           | Love. Angel. Music. Baby. | 48            | Gwen Stefani    |
| 175          | Collage (EP)   | 32            | Halsey          |
| 227          | Manic          | 32            | Halsey          |
| 211          | Single         | 32            | Halsey          |
| 58           | Evolve         | 17            | Imagine Dragons |
| 70           | Night Visions  | 17            | Imagine Dragons |
| 153          | Control        | 70            | Janet Jackson   |
| 79           | Janet Jackson's Rhythm Nation 1814 | 70            | Janet Jackson   |
| 207          | janet.         | 70            | Janet Jackson   |
| 185          | My Kinda Party | 88            | Jason Aldean    |
| 15           | Old Boots, New Dirt | 88            | Jason Aldean    |
| 64           | Wide Open      | 88            | Jason Aldean    |
| 149          | Jason Derulo   | 31            | Jason Derulo    |
| 121          | Single         | 31            | Jason Derulo    |
| 252          | Tattoos/Talk Dirty | 31            | Jason Derulo    |
| 190          | Love?          | 41            | Jennifer Lopez  |
| 96           | On the 6       | 41            | Jennifer Lopez  |
| 184          | Get Lifted     | 23            | John Legend     |
| 9            | Love in the Future | 23            | John Legend     |
| 242          | Selma (Soundtrack) | 23            | John Legend     |
| 220          | American IV: The Man Comes Around | 76            | Johnny Cash     |
| 84           | Ring of Fire: The Best of Johnny Cash | 76            | Johnny Cash     |
| 5            | With His Hot and Blue Guitar | 76            | Johnny Cash     |
| 139          | FutureSex/LoveSounds | 50            | Justin Timberlake |
| 250          | Justified      | 50            | Justin Timberlake |
| 155          | The 20/20 Experience | 50            | Justin Timberlake |
| 106          | Golden Hour    | 93            | Kacey Musgraves |
| 68           | Same Trailer Different Park | 93            | Kacey Musgraves |
| 245          | Graduation     | 20            | Kanye West      |
| 128          | Late Registration | 20            | Kanye West      |
| 126          | My Beautiful Dark Twisted Fantasy | 20            | Kanye West      |
| 216          | Be Here        | 89            | Keith Urban     |
| 187          | Golden Road    | 89            | Keith Urban     |
| 120          | Ripcord        | 89            | Keith Urban     |
| 167          | Breakaway      | 47            | Kelly Clarkson  |
| 75           | Stronger       | 47            | Kelly Clarkson  |
| 176          | Eyes That See in the Dark | 79            | Kenny Rogers    |
| 189          | Kenny Rogers' Greatest Hits | 79            | Kenny Rogers    |
| 235          | The Gambler    | 79            | Kenny Rogers    |
| 114          | Lady Antebellum | 98            | Lady A          |
| 102          | Need You Now   | 98            | Lady A          |
| 193          | Own the Night  | 98            | Lady A          |
| 233          | A Star Is Born (Soundtrack) | 6             | Lady Gaga       |
| 78           | Born to Die    | 37            | Lana Del Rey    |
| 113          | The Great Gatsby (Soundtrack) | 37            | Lana Del Rey    |
| 125          | 7 (EP)         | 52            | Lil Nas X       |
| 197          | Pain Killer    | 99            | Little Big Town |
| 188          | The Breaker    | 99            | Little Big Town |
| 228          | Tornado        | 99            | Little Big Town |
| 246          | Melodrama      | 21            | Lorde           |
| 67           | Pure Heroine   | 21            | Lorde           |
| 87           | Crash My Party | 87            | Luke Bryan      |
| 181          | Tailgates & Tanlines | 87            | Luke Bryan      |
| 66           | I'm Breathless | 64            | Madonna         |
| 134          | Like a Virgin  | 64            | Madonna         |
| 180          | Hands All Over (Re-release) | 16            | Maroon 5        |
| 21           | Songs About Jane | 16            | Maroon 5        |
| 8            | Single         | 34            | Marshmello      |
| 154          | Single         | 34            | Marshmello      |
| 236          | Single         | 34            | Marshmello      |
| 191          | Title          | 53            | Meghan Trainor  |
| 65           | I'm a Lonesome Fugitive | 80            | Merle Haggard   |
| 115          | Mama Tried     | 80            | Merle Haggard   |
| 57           | Okie from Muskogee | 80            | Merle Haggard   |
| 129          | Bad            | 62            | Michael Jackson |
| 253          | Thriller       | 62            | Michael Jackson |
| 140          | Bangerz        | 22            | Miley Cyrus     |
| 7            | Endless Summer Vacation | 22            | Miley Cyrus     |
| 100          | The Time of Our Lives (EP) | 22            | Miley Cyrus     |
| 105          | Kerosene       | 92            | Miranda Lambert |
| 29           | Revolution     | 92            | Miranda Lambert |
| 85           | Wildcard       | 92            | Miranda Lambert |
| 99           | Country Grammar | 51            | Nelly           |
| 171          | Nellyville     | 51            | Nelly           |
| 162          | No Strings Attached | 57            | NSYNC           |
| 42           | NSYNC          | 57            | NSYNC           |
| 150          | Midnight Memories | 55            | One Direction   |
| 63           | Up All Night   | 55            | One Direction   |
| 81           | Greatest Hits... So Far!!! | 36            | P!nk            |
| 158          | M!ssundaztood  | 36            | P!nk            |
| 138          | The Truth About Love | 36            | P!nk            |
| 48           | Meltdown (EP)  | 40            | Pitbull         |
| 231          | Planet Pit     | 40            | Pitbull         |
| 123          | Rebelution     | 40            | Pitbull         |
| 111          | Hollywood's Bleeding | 29            | Post Malone     |
| 165          | Spider-Man: Into the Spider-Verse (Soundtrack) | 29            | Post Malone     |
| 38           | Stoney         | 29            | Post Malone     |
| 218          | Parade         | 66            | Prince          |
| 103          | Purple Rain    | 66            | Prince          |
| 39           | A Night at the Opera | 61            | Queen           |
| 32           | News of the World | 61            | Queen           |
| 196          | The Game       | 61            | Queen           |
| 225          | Feels Like Today | 100           | Rascal Flatts   |
| 93           | Me and My Gang | 100           | Rascal Flatts   |
| 16           | Gloria         | 18            | Sam Smith       |
| 122          | The Thrill of It All | 18            | Sam Smith       |
| 179          | Rare           | 27            | Selena Gomez    |
| 45           | Revival        | 27            | Selena Gomez    |
| 192          | Stars Dance    | 27            | Selena Gomez    |
| 2            | Listen Up! The Official 2010 FIFA World Cup Album | 39            | Shakira         |
| 223          | Oral Fixation Vol. 2 | 39            | Shakira         |
| 217          | Come On Over   | 83            | Shania Twain    |
| 142          | 1000 Forms of Fear | 19            | Sia             |
| 137          | This Is Acting | 19            | Sia             |
| 202          | Spice          | 59            | Spice Girls     |
| 104          | Spiceworld     | 59            | Spice Girls     |
| 195          | Songs in the Key of Life | 69            | Stevie Wonder   |
| 141          | Talking Book   | 69            | Stevie Wonder   |
| 182          | Fearless       | 84            | Taylor Swift    |
| 80           | Taylor Swift   | 84            | Taylor Swift    |
| 201          | Help!          | 60            | The Beatles     |
| 234          | Let It Be      | 60            | The Beatles     |
| 204          | Single         | 60            | The Beatles     |
| 90           | Bouquet (EP)   | 35            | The Chainsmokers |
| 76           | Collage (EP)   | 35            | The Chainsmokers |
| 36           | Memories...Do Not Open | 35            | The Chainsmokers |
| 159          | All I Want     | 90            | Tim McGraw      |
| 183          | Damn Country Music | 90            | Tim McGraw      |
| 50           | Live Like You Were Dying | 90            | Tim McGraw      |
| 136          | Foreign Affair | 71            | Tina Turner     |
| 237          | Private Dancer | 71            | Tina Turner     |
| 73           | Confessions    | 42            | Usher           |
| 108          | Versus (EP)    | 42            | Usher           |
| 89           | The Bodyguard (Soundtrack) | 65            | Whitney Houston |
| 161          | Whitney        | 65            | Whitney Houston |
| 92           | Whitney Houston | 65            | Whitney Houston |
| 169          | Always On My Mind | 78            | Willie Nelson   |
| 168          | Honeysuckle Rose (Soundtrack) | 78            | Willie Nelson   |
| 82           | Red Headed Stranger | 78            | Willie Nelson   |
| 144          | You Get What You Give | 97            | Zac Brown Band  |
| 178          | Fifty Shades Darker (Soundtrack) | 26            | Zayn            |
| 148          | Mind of Mine   | 26            | Zayn            |
| 214          | Single         | 26            | Zayn            |
+ ------------ + -------------- + ------------- + --------------- +
200 rows
```

This query is useful for finding albums and artists that are less popular. Artists may use this information to find out what types of songs are not popular with fans. Fans may use this information to find underground artists that they have not heard of before.

Query 10
Returns the ID number, name, and number of Taylor Swift concerts attended for fans who have attended more than 5 Taylor Swift concerts.
  ConcertsAttended.fanID,
  Fan.fanName,
  COUNT(*) AS times_attended
FROM ConcertsAttended
JOIN Concert
  ON ConcertsAttended.date = Concert.date
 AND ConcertsAttended.startTime = Concert.startTime AND ConcertsAttended.endTime = ConcertsAttended.endTime
JOIN Fan ON Fan.fanID = ConcertsAttended.fanID
WHERE Concert.headlinerArtistID = 1
GROUP BY ConcertsAttended.fanID, Fan.fanName
HAVING COUNT(*) > 5
ORDER BY times_attended DESC;

This query is useful because Taylor Swift is known for having one of the most dedicated fan bases of any artist. Knowing who her biggest fans are and who is most likely to attend her concerts is very useful for her when she releases new music or goes on tour. Her managers and producers can target these fans since they are most likely to make a purchase.
## Database Information

