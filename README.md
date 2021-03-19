# Wrangle-and-Analyze-Data
The dataset that I will be wrangling, analyzing and visualizing is the tweet archive of Twitter user @dog_rates, also known as WeRateDogs. WeRateDogs is a Twitter account that rates people's dogs with a humorous comment about the dog. These ratings almost always have a denominator of 10. The numerators, though? Almost always greater than 10. 11/10, 12/10, 13/10, etc. Why? Because "they're good dogs Brent." WeRateDogs has over 4 million followers and has received international media coverage.

## Gathering Data
I gathered WeRateDogs twitter archive data by downloading the file provided to me via link by the Udacity and then loaded that archive data in csv format.
I gathered WeRateDogs tweet image predictions hosted on Udacity's servers (in tsv format) by dowloading that file programmatically using requests library.
I gathered WeRateDogs twitter account additional data (retweet count and favorite ("like") count) through Twitter API and the python tweepy library. Using the tweet IDs in the WeRateDogs Twitter archive, I query the Twitter API for each tweet's JSON data using tweepy library and stored each tweet's entire set of JSON data in a file called tweet_json.txt file. Finally, I read the twitter json data from tweet_json.txt file by converting each json string into python dictionary and appending them to a list (row by row) and this list of dictionaries was eventually converted to a python pandas DataFrame.

## Assessing Data
After performing visual and programmatic assessments of datasets I found following quality and tidiness issues.

Quality issues
- Completeness: Missing values of dog stages and dog names (can't clean)
- Accuracy: Replace missing values named as None with NaN in name and dog stages columns
- Validity: Erroneous datatypes of tweet id, it should be string not integer
- Accuracy: Investigate name column for incorrect names as some of the dog names seemed inaccurate (all, my, not, a, an, the, by, such)
- Consistency: Only those tweet ids who have image predictions in the image prediction table
- Accuracy: Inaccurate values of rating denominator
- Accuracy: Inaccurate values of rating numerator
- Validity: Timestamp, retweeted_status_timestamp datatype is of string, it should be datetime
- Consistency: We want original ratings so remove tweet ids which are retweets

Tidiness issues
- Melt the columns doggo, floofer, pupper and puppo as these column headers are values instead of variable names, variable name is dog stage in the archive table (wrd_archive)
- Split text column of archive table into two separate columns (tweet_text and tweet_url)
- Merge the archive (wrd_archive), archive additional (wrd_archive_add) and image prediction (wrd_image_prediction) tables
