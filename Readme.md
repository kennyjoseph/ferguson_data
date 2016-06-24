# Ferguson Twitter Data

This dataset is a collection of 3,164,569,430 (3.1B) tweets from ~1.2M Twitter users who were actively engaged in discussions about events surrounding the deaths of Eric Garner and Michael Brown.

# Collection methodology
Approximately a week after the Michael Brown tragedy, I collected data for approximately two weeks using a keyword search on the Twitter Streaming API with terms relevant to the situation (“ferguson”, “michael brown”, “darren wilson”). I then stopped collecting data until the grand jury investigation finished, at which point I used several connections to the streaming API to search another set of relevant terms for approximately a week (#fergusondecision, McCulloch, brown, ferguson, michael brown, berkeley, darren wilson, police). Following the Eric Garner grand jury conclusion, I used the keywords “garner” and “eric garner” to search the Streaming API, again for approximately a week. I also developed a different keyword set to continuously capture data from the Streaming API around that time (icantbreathe , i cant breathe, garner, michael brown, freedom plaza, blacklivesmatter, alllivesmatter), which I ran for around five weeks.

On December 24th, 2014, I began using the Twitter REST API to extract the full set of tweets for all users that had sent at least five tweets in the full set of collected data. In total, there were just over 1.2M such users. I also extracted their follower and following relationships. Due to other uses of the machine on which this processing was occurring, collection took approximately five weeks. There are two restrictions to this collection process. First, Twitter only allows you to download historical data from users who are still active and those whose accounts are still public. Second, Twitter only allows you to see the previous 3200 tweets from any given user. Thus, for users like news agencies, who tweet frequently, I was not able to obtain all of their historical tweets. Regardless, I have the full, or nearly the full, timelines for approximately 1.2M users who can be expected to have tweeted actively about the Michael Brown and Eric Garner tragedies, as well as their follower and following relationships.

# Usage "Agreement"

The dataset is provided as-is, no additional information will be provided. If you use this dataset, please send me an email to let me know (josephkena _a_ gmail _d_ com) and please cite the following publication which first introduces and uses the dataset:

```
@inproceedings{joseph_exploring_2016,
	title = {Exploring patterns of identity usage in tweets: a new problem, solution and case study},
	shorttitle = {Exploring patterns of identity usage in tweets},
	url = {http://dl.acm.org/citation.cfm?id=2883027},
	urldate = {2016-06-22},
	booktitle = {Proceedings of the 25th {International} {Conference} on {World} {Wide} {Web}},
	publisher = {International World Wide Web Conferences Steering Committee},
	author = {Joseph, Kenneth and Wei, Wei and Carley, Kathleen M.},
	year = {2016},
	pages = {401--412},
	file = {Snapshot:/Users/kennyjoseph/Library/Application Support/Zotero/Profiles/1vik5dqf.default/zotero/storage/5UUKWU6H/citation.html:text/html}
}
```

# Data

There are three data files for this dataset:

- https://dl.dropboxusercontent.com/u/53207718/ferguson_data/all_ferguson_tweet_ids.txt.gz - (~24G) - IDs for all tweets from all users in the dataset, one per line
- https://dl.dropboxusercontent.com/u/53207718/ferguson_data/follower_network.txt.gz - (~17G) - Followers for all users in the dataset (file detail below)
- https://dl.dropboxusercontent.com/u/53207718/ferguson_data/friend_network.txt.gz - (~5.8G) - Friends for all users in the dataset

The format of the friend and follower network files is as follows:
```
user_id_1 <tab> friend1_id friend2_id friend3_id ...
user_id_2 <tab> friend1_id friend2_id friend3_id ...
```

# Recollection of tweets from IDs

Abiding by Twitter's Terms of Service, this dump only provides IDs of tweets in the dataset. In order to "hydrate" those tweet IDs, or in other words, to collect the actual tweets, you'll have to access the API. Unfortunately, in order to collect all tweets with a single, serial connection to the API would take a very, very long time (on the order of years w/ current API restrictions).

You therefore have a few options that I know of (but please tell me if you have a better approach!):

- subselect users of interest (from the networks) and then re-collect data from these users yourself
- Parallelize the download using your own approach, e.g. via multiple connections using ```tweepy```
- Parallelize the download using a package I have developed called ```twitter_dm```, available on GitHub at https:www.github.com/kennyjoseph/twitter_dm .  The script ```examples/collect_tweets.py``` in the ```twitter_dm``` package provides an easy way to leverage all connections to parallelize downloading of the tweet IDs.

Note that the last two approaches (and probably the first) requires multiple connections to the API.
