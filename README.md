# Wayback Machine Webshots Metadata Search
A dataset of 2012 Webshots profile metadata from the Internet Archive's Wayback Machine for the purpose of enabling gallery searches.

This project consists of an archive of text-only .txt copies of the text contained within each Webshots profile page that the Wayback Machine has archived from 2012 via an Archive Team crawl that was made weeks before the website closed. The Wayback Machine hosts a significant amount of former Webshots data (just over 1.7 million profiles and their associated content) but does not provide any built in way of searching for content besides allowing you to search for archived URLs. The Webshots .WARC files hosted on the Internet Archive contain all of the image content and other assets and as a result are massive in size, whereas this profile page metadata dataset is tiny by comparison and designed for the purpose of searching.

I would recommend using either a terminal command to search for gallery terms or alternatively a program like GrepWin. When running from a command line, ensure that the command is from the root directory containing each alphabet, and ensure it is configured to search within subdirectories. On MacOS the mdfind command is by far the fastest but it relies on the Spotlight function, which is likely to take several hours to cache the data after downloading and extracting. Grep is a more reliable but much slower option on Unix systems. Ensure that whatever search command you use outputs the directory path of each result, which will contain the profile name.

An mdfind command on MacOS should look like the following:

`mdfind \"text phrase\"  -onlyin "/pathto/webshotscrawl/users"`

A Unix grep command (which will hang for a long time as it searches for content; depending on the speed of your system this could take up to several hours) on a system running MacOS or Linux should be in this format:

`grep -r "text phrase" "/pathto/webshotscrawl/users"`

On Windows systems this should work, although I haven't tested it:

`cd "C:\pathto\webshotscrawl\users"`

`findstr /S /C:"text phrase" *.txt`

To load a profile containing a gallery of interest, copy the profile name listed in the search results (eg: `pathto/*profilename*/index.txt`) and enter in your web browser's URL bar `https://web.archive.org/web/20120101/http://webshots.com/user/*profilename*`. The Wayback Machine will then modify the URL to the appropriate timestamp from 2012 that it has archived and load the profile page, which you will be able to explore.



Current limitations include the following:

* Other text besides gallery names, including the names of Webshots interface links, is stored in each .txt file. You should be careful when performing a batch search of the files not to specify any of the single words or phrases that appear on every profile page (eg: Webshots, log in, photos, animals, popular etc). I may be able to perform some batch modifications to the .txt files at some point in the future to narrow down the content of the files to just gallery names and dates, which should also significantly reduce the size of the dataset as well as making it more reliable for certain terms.
* A small number of the circa 1.7 million profiles were not successfully scraped, either due to a server error (the Internet Archive's servers are not the most reliable) or the server's rate limiter being briefly hit. The number of profiles affected is reasonably small and I would estimate is no more than a couple of thousand thousand out of around 1.7 million, but it might be possible for me to add these later. If you can't find your own former profile anywhere in the dataset then it's much more likely simply not to have been salvaged by Archive Team in the weeks leading up to Webshots closing.
* Pages on the 2012 Webshots site are very slow to load on the Wayback Machine. This is beyond my control.
