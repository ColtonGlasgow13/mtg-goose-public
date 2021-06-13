## Navigation
[**Previous Project**](https://coltonglasgow13.github.io/mtg-python-public "mtg-python")&nbsp;&nbsp;&nbsp;&nbsp;|||&nbsp;&nbsp;&nbsp;&nbsp;[**Home**](https://coltonglasgow13.github.io/ "Homepage")&nbsp;&nbsp;&nbsp;&nbsp;|||&nbsp;&nbsp;&nbsp;&nbsp;[**Next Project**](https://coltonglasgow13.github.io/goose-stock/ "goose-stock")

# Summary

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;My previous project collected limited amounts of data about collectible card prices, but I wanted a system that would provide all the data I could want in terms of investment and resale decisions. Therefore, I developed an application to scrape data from a variety of sources and store it in a remotely hosted relational database, where I then used it for analysis and visualization. Through the support of this application, I have been able to sustain my collectible resale business ([Household Gaming](https://www.ebay.com/fdbk/feedback_profile/household_gaming)) for years by making data-driven decisions and building my understanding of the market from the bottom up.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This project took a very significant amount of time and effort to complete, as I had to work through some of the struggles of larger applications while exploring new environments and tools. Before this project I had never controlled a server, programmed in SQL, designed a database, scraped from javascript-based sites, or allowed a program to make investment decisions for me, so the process was eye-opening in many ways. But by the time it was complete, I had used all of these skills to develop a unique application, field-tested to have the ability to generate a stronger return on investment than I could have ever achieved manually.

# Groundwork

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In order to gather consistent data, collection needs to be automated, but running a script through the Windows Task Scheduler wasn't cutting it. It didn't run when my computer wasn't on, and even when it was it often didn't run consistently and took up too many system resources. In addition, given the amounts of data that I wanted to collect and use, a remote server was the best option to contain my project. However, I had no experience with this process and no server to use, so I would have to build it up from scratch.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;I managed to claw through the process of setting up a remote server with the basics available to me ([this guide](https://data36.com/data-coding-101-install-python-sql-r-bash/) and others on data36 were a lifesaver, I highly recommend using it if you are trying a similar project), including a postgresql server and jupyter notebook, both of which I could access from my pc, making interaction more efficient.
