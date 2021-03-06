## Month #4
### Week #13
- - -
#### Monday April 10, 2017
* **Goals**:
	* ~~Finish gift cards modelling for Merchant Data Warehouse.~~
	* Start on other data projects.
* **Accomplishments**:
	* Went through a clustering and regression modelling tutorial in python.
* **Feedback**:
	1. When you expose a schema vs a report to the consumers it's very different.  
		* Reportify:  
    		You are only exposing the final product so data can't be as raw.  
            Ex. **type** column in the model can be *lowercase* but in reportify it should be *uppercase*. 
		* Merchant Data Warehouse:  
			You are exposing the raw models to the merchants, therefore you should think about how you would use these models to build the reportify reports.  
            Ex. you should keep **datetimes** in *UTC* time instead of shop timezone. This is how you would see them in the database.  
	For next time you can keep the logic in first layer (starscream) the same, but when you expose the schema in reportify or in the UI layer you can reference it differently.
	2. Writing better documentation for github PRs. More to the point and descriptive. 
 
	**What are you trying to accomplish with this PR?**  
	This PR will create a model **gift_card_transactions__daily_rollup** that will rollup gift_card_transactions. Unlike Reportify, this model will disregard shop timezones as we want to expose UTC timezones in the data warehouse.

	**How is this accomplished?**  
This PR creates a new model, **gift_card_transactions__daily_rollup**, which unions the following stages from gift_card_transactions, and then aggregates on a per day granularity. Dates with no transactions are filled in.

        * **GiftCardsIssued** (gift cards that were given out by the merchant.)
        * **GiftCardsSold** (gift cards that were bought.)
        * **GiftCardsDisabled** (gift cards that are past the disabled_at date.)
        * **GiftCardsRefunded** (orders that were purchased by gift cards but then refunded for any reason.)
        * **GiftCardsRedeemed** (orders that were purchased by gift cards.)

	Tests have been added for the new stages, as well as the full pipeline.
    
#### Tuesday April 11, 2017
* **Goals**:
	* Inventory history.
	* Migrate gift cards.
	* gift cards documentations.
	* Gift cards on shopify core.
* **Accomplishments**:
* **Feedback**:
	1. Catch up with people, it is more personal than just talking to someone on facebook. Get more friends Eric.
	2. Spark SQL at Shopify:
		* [daily_partner_accumulating_facts_builder_v2](https://github.com/Shopify/starscream/blob/master/shopify/facts/daily_partner_accumulating_facts_builder_v2.py#L62)  
		![alt text](https://raw.githubusercontent.com/ericxiao251/Python-Sugar/master/Spark%20Sugar/Spark%20SQL.png?token=AJTnLrQkCgPpUxr8HFn3ILRBTErale1Oks5Y-C-1wA%3D%3D "Slack discussion")  
	3. [online store page views](https://github.com/Shopify/starscream/tree/a97197315385fd128482b4fc9178f1b7a407fe42/shopify/views/reportify/online_store)
    Great example of big data usage with incremental jobs.
    4. Look at spark files for how to work with adding/deleting columns from input contract.

#### Wednesday April 12, 2017
* **Goals**:
	* Back burners:
		* Migrate gift cards.
		* gift cards documentations.
    * Current:
	    * ~~Work on online store model in MDW.~~
* **Accomplishments**:
* **Feedback**:
    1. When a `scala function not found` or `JavaPackage`:
    	* run `cd scala && sbt assembly`.
        * you will need to build the scala functions if any new ones are added.

#### Thrusday April 13, 2017
* **Goals**:
	* Back burners:
		* Migrate gift cards from MDW to Reportify.
		* Inventory reconciliation tool.
    * Current:
		* Gift cards documentations.  
		  Use these previous documentations as reference:
          1. [PR](https://github.com/Shopify/documentation/pull/9442)
          2. [Google Docs](https://docs.google.com/document/d/1RntG8DNeVjvAGeK1cOQgXy9kfjeksISWyRdRPaDoWy4/edit)
	    * Online store cart --> [PR](https://github.com/Shopify/starscream/pull/17037)  
          Use that spicy contract addition/subtraction in **[online store page views](https://github.com/Shopify/starscream/tree/a97197315385fd128482b4fc9178f1b7a407fe42/shopify/views/reportify/online_store)**

#### Friday April 14, 2017
* **Goals**:
	* ~~Read Mining the Social Media - Chapter 1.~~
	* Create a twitter API.
* **Feedback**:
	* How to write a restful API [link](https://www.quora.com/What-is-a-good-Python-framework-for-building-a-RESTful-API)

#### Saturday April 15, 2017
* **Goals**:
	* Work on Chapter 1.

#### Sunday April 16, 2017
How to procrastinate.

#### Thrusday April 20, 2017
* **Goals**:
	* Look at NLP --> [spaCy](https://github.com/explosion/spaCy)
	* Finish looking at online store pageviews.
	* Transfer all of Spark and Python sugar to notebooks.
* **Accomplishments**:
	* Understanding Python a lot more.
* **Backlog**:
	* What is **Multiple Inheritance** in Python? 
	* How do you put stuff in the env in Spark, how does this work?

#### Saturday April 22, 2017
* **Goals**:
	* Resume projects:
		* Work through spaCy NLP and Yelp data --> [link](http://nbviewer.jupyter.org/github/skipgram/modern-nlp-in-python/blob/master/executable/Modern_NLP_in_Python.ipynb)
		* Find Big Data University's R cusine classifier.
		* Finish Twitter API data.
    * PyData conference, look through those examples --> [link](https://pydata.org/dc2016/schedule/)

#### Monday April 24, 2017
* **Backlog**:
	* Why are you so sloppy?
	* When you learning ML, concepts are clear, but library functionality are not. Not sure what this library can and can't do.

#### Thrusday April 27, 2017
* **Checklist**:
	1. fix generated schedule file
	2. ship `online_store_pageviews` docs
	3. edit `online_store_cart_additions` docs —> ship
	4. edit `online_store_cart_additions` code —> ship
* **Feedback**:
	* `git commit --amend --reuse-message=HEAD` this adds any changes to your previous commit.