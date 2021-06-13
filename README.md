## Navigation
[**Previous Project**](https://coltonglasgow13.github.io/mtg-python-public "mtg-python")&nbsp;&nbsp;&nbsp;&nbsp;|||&nbsp;&nbsp;&nbsp;&nbsp;[**Home**](https://coltonglasgow13.github.io/ "Homepage")&nbsp;&nbsp;&nbsp;&nbsp;|||&nbsp;&nbsp;&nbsp;&nbsp;[**Next Project**](https://coltonglasgow13.github.io/goose-stock/ "goose-stock")

# Summary

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My previous project collected limited amounts of data about collectible card prices, but I wanted a system that would provide all the data I could want in terms of investment and resale decisions. Therefore, I developed an application to scrape data from a variety of sources and store it in a remotely hosted relational database, where I then used it for analysis and visualization. Through the support of this application, I have been able to sustain my collectible resale business ([Household Gaming](https://www.ebay.com/fdbk/feedback_profile/household_gaming)) for years by making data-driven decisions and building my understanding of the market from the bottom up.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This project took a very significant amount of time and effort to complete, as I had to work through some of the struggles of larger applications while exploring new environments and tools. Before this project I had never controlled a server, programmed in SQL, designed a database, scraped from javascript-based sites, or allowed a program to make investment decisions for me, so the process was eye-opening in many ways. But by the time it was complete, I had used all of these skills to develop a unique application, field-tested to have the ability to generate a stronger return on investment than I could have ever achieved manually.

# Groundwork

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In order to gather consistent data, collection needs to be automated, but running a script through the Windows Task Scheduler wasn't cutting it. It didn't run when my computer wasn't on, and even when it was it often didn't run consistently and took up too many system resources. In addition, given the amounts of data that I wanted to collect and use, a remote server was the best option to contain my project. However, I had no experience with this process and no server to use, so I would have to build it up from scratch.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I managed to claw through the process of setting up a remote server with the basics available to me ([this guide](https://data36.com/data-coding-101-install-python-sql-r-bash/) and others on data36 were a lifesaver, I highly recommend using it if you are trying a similar project), including a postgresql server and jupyter notebook, both of which I could access from my pc, making interaction more efficient. Now that I had a platform to work from, I could get started developing functionality.

# Database Structure

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This was my first time working with a database, so I wasn't aware of many existing conventions for database organization. However, the schema that I developed was essentially in line with common data warehousing structures, so I ended up satisfied with its capabilities.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A central, recurring issue concerning the development of applications that work with collectibles is that there is not a strong centralized resource for information about these collectibles. The stock market has SEC's EDGAR and the consistent reports of different exchanges, but for collectibles I had to rely on independently maintained sources such as [MTGJSON](https://mtgjson.com/). MTGJSON was an essential resource for developing not only my application, but also a variety of well-known and widely used public applications such as [Scryfall](https://scryfall.com/), [Cardmarket](https://www.cardmarket.com/en), and [Cardsphere](https://www.cardsphere.com/). With it, I had access to detailed information about every Magic: the Gathering card in existance, all ready to download and use, which allowed my database to track every single card without the need to manually input their information.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The core of my database provides a unique id for every card, but even using that, normalization of the incoming data was a substantial roadblock. There are many different variants and printings of cards with the same name, and every site that I needed data from uses different naming and labeling conventions, so I couldn't scrape information directly into tables. To get around this problem, I developed a standardization system which contained the alternate names for each card depending for every site being used, and referenced them whenever data was read in. Now that I had established storage for the data, I needed to collect it.

# Data Collection

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Again, there is no centralized resource for collectible card data, so as I wanted to monitor many different sources I needed to scrape the data from each source individually. There are hundreds of companies that sell collectible cards, and even though the focus of the application is on Magic: the Gathering products, there are still too many to track. Therefore I chose some of the most crucial sources to work with under the following criteria. First, if I intended to sell cards using a platform, it would of course be essential to keep track of that platform's prices. In addition, I wanted to track a variety of buylists, because as described in my previous project, buylists represent a safe backbone for the price of cards. I chose some of the largest and most popular buylists, because they are the most likely to want to buy large quantities of cards and are the most dependable.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Some buylists, such as [Card Kingdom's Buylist](https://www.cardkingdom.com/purchasing/mtg_singles?filter[sort]=price_desc), are html-based, so I could scrape them via Python's built-in [Requests](https://docs.python-requests.org/en/master/) package to pull the sites and the [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) package to access the data more efficiently. I standardized all the cards and processed their information using a [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html) DataFrame, and employed [psycopg2](https://www.psycopg.org/docs/) to send it to the table corresponding to the company's buylist data.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Other buylists, such as Miniature Market's (while it still existed), presented their buylist prices in the form of Javascript, so I couldn't scrape them as efficiently and directly. I was forced to use [Selenium](https://www.selenium.dev/), a WebDriver that allowed my program to appear as a person using a browser, which them allowed me access to pricing. This process was slower and harder to design, so it was only used when necessary.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Finally, thankfully [TCGPlayer](https://www.tcgplayer.com/) allowed me access to their internal price API for private use as a seller on their platform. TCGPlayer is one of the largest marketplaces for collectible cards and allows anyone to open a storefront, so scraping it would have been very slow and inefficient. Thanks to their API access, I could quickly acquire the data I needed for every card sold on this large platform, which is often treated as the "market price" for cards in the US.

# Data Application

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Now that I was collecting data for each of these metrics daily, what could I do with it? Well, first of all, I could visualize any data that I wanted to observe trends or price history in an intuitive way.

> Data from multiple sources collected over months for every card in the _Ice Age_ set, which released in 1996.
> 
> ![image alt ><](/Images/IceAgeCardValueOverTime.png)
