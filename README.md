# pentaho_scrape_original_records
Pentaho Data Integration (PDI) Job Transformation Scrape Original Records

The project jobs and transformations generate a list of URLs, extract the HTML from the site pages, and parse the information into fields, such as date, location, contact, and content. This project was created in an effort to consume the Original Records into a more consumable data format, with distinct columns.  The site content is not well-formed, hence the need to parse the HTML using numerous JavaScript rules.  

Requirements:
jsoup - download jsoup-1.11.2.jar and place within your local Pentaho\{version}\data-integration\lib directory.  
If PDI is running, restart it.

Potential Requirements:
The security certificate for the source URL (https://ehistory.osu.edu/books/official-records) may need to be installed.

Procedure:
1.  Place the job and transformation files into your local Pentaho\{version}\data-integration\samples\transformations directory.
2.  Place the csv files into your local Pentaho\{version}\data-integration\samples\transformations\files directory.
3.  Start Pentaho Data Integration (PDI), and open job_generate_urls.kjb.
4.  In PDI, select Edit, Set Environment Variables and enter the following:

    NAME        VALUE
    page_start  0979
    page_stop   0989
    serial      099
    url         https://ehistory.osu.edu/books/official-records
    
5.  Once the environment variables are set, start job_generate_urls.kjb.

Results:
1.  The job will generate a list of URLs using the range specified in the variables, and append them to the file url_list.csv.
    This file is simply used as a source for job_scrape_original_records.kjb.
2.  Content from each of the URLs will be extracted and parsed, then appeneded to the file original_records.csv.

Tip:  As long as URLs are listed in the file url_list.csv, then transformation_scrape_original_records.ktr could be run manually (without running the job).  The job is simply to prepare a range of URLs easily.

Notes:  
  -I suggest a maximum range of 200 pages.
  -This project could be easily modified to extract and parse content from HTML sites that have incremental page numbers in the URL path.

