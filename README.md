# Using-CSV-Writer-to-bridge-Python---Javascript-gap
This inquiry report details how I used CSV to convert a matrix of rows of data, in the form of a list of lists in Python, into a text file holding all of the data individually as lists. The text file containing the scraped data obtained from the Python script can then be used by javascript to produce pinpoint markers on the google map.

#Problem
I am producing a world music map via the Google Maps Javascript API. Obviously I am writing the script to build the Google map in Javascript, but I am new to using javascript. I have already written a script in Python that accesses the EchoNest database and scrapes meta-data for artist, song, latitude, and longitude for each of the songs in the 10,000 song EchoNest "Million Song Subset". That script places the meta-data for each song into a 4-item vector that is inputted as a list of lists in Python format and from there the specific data for each song is easily accessible and usable, in Python. The issue that has presented itself is that in the javascript program I am writing to produce the Google map, in order to produce interactive pinpoint markers at each of the locations where the songs originated I need to access the data that is produced and held by the Python script. The Javascript program cannot effectively communicate with Python to obtain that data, so I need to find a way to create a bridge between the two and output the scraped meta-data from the Python script and use it as input into the Google map script to produce those markers.

#Research Questions
1. How can I transfer the data produced by my Python script, getTrackData.py, to my Javascript that needs that data to produce pinpoint markers on a Google map?
2. Upon research into Javascript and the Google Maps API I've found out that if I can produce a text file holding the data, that the javascript can take the data from the text file and produce pin points based on the respective latitude/longitude data. Is there a way to produce a text file containing the scraped track meta-data from the Python script?

#Resources
[CSV File Reading and Writing](https://docs.python.org/2/library/csv.html)

#Mini-Abstract of Relevance for CSV File Reading and Writing
This document provided by Python docs details the CSV module. CSV (Comma Separated Values) provides a means for reading and writing to files which are in an iterable format. In Python if you have a structure that serves as a lists of lists, separated by commas, a CSV reader/writer can parse that file and output that file to several different desired formats. The CSV format is the most desired format for importing and exporting from spreadsheets and databases. CSV offers many different specifiers for how a reader or writer parses a file, including: writerow(), writerows(), readrow(), readrows(), which are very helpful when attempting to write the data held within a matrix (list of lists) to an output file like a text file. CSV directly solves the problem I was having with getting the data I needed from the Python script transferred to the Javascript where I need it to produce the pinpoint markers on the Google map. With the use of the CSV module I was able to write each 4-item vector row of the trackData matrix to a text file that I am able to use as input for the Javascript by accessing each vector individually and producing a pinpoint marker based accordingly to the latitude and longitude data provided by it. CSV served as the bridge that joined the data I obtained via the trackData.py script with the Google map javascript that needed it to produce pinpoint markers for each song. The list-formatted text file produced by the CSV writer is what made producing the song-positioned pinpoint markers on the Google map possible. This resource answers questions 1 and 2.

#How I used CSV
```
def write_to_txt():
        tracks = getTrackData('MillionSongSubset')
        with open('trackData.txt', 'wb') as f:
                writer = csv.writer(f)
                writer.writerows([tracks])
```
Explanation: The code above produces a list of lists named 'tracks' that is a matrix holding all of the desired track data from the songs in the given directory of music files 'MillionSongSubset'. Once that matrix is populated, a CSV writer is used to traverse the matrix row-by-row and write all rows to the output file given 'trackData.txt'. Upon this function completing execution, the trackData.txt file now holds all of the data produced by the python script and is readily usable by the javascript as input to produce pinpoint markers.
