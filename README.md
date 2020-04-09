# Weibo-Social-Media-Analytics
The project was for the class MSBA Social Media Analytics(2019-2020) provided by the Master of Science in Business Analytics from the University of Hong Kong and was done by( in alphabetical order) Lin Liwei, Lin Hongying, Wang Yanyuan, Wang Yang, Zhang Xinyi, Zhou Zezhong, Zhong Qitong. In this project, we cloned and edited others' code in Github.com. Because the project is not for real business case, so we didn't notice them but list them at the bottom of the README file for reference.
# 1 Project Idea 
Product Promotion in social media platforms is very popular in recent years. According to TopKlout (2019), in 2020, the share of the social media market in the e-market will increase by 11.5%, and the market value of blogger-related e-market will reach 3,000,000,000 RMB. The beauty industry, in particular, is embracing this influencer marketing strategy. More and more cosmetic brands are partnering with beauty influencers to share and promote their products on social media platforms. Based on general knowledge, the number of one blogger’s active followers are positively correlated with his/her promotion effect. However, there might be some other factors, such as product information and post content, that would influence bloggers’ promotion effect. Thus, it might be not accurate enough when brands choose bloggers only based on their social media follower numbers. The purpose of this project is to explore a scientific model to select the best-performance beauty influencers for beauty brands to cooperate with regarding their product information.  

# 2 Code Introduction
Note that the programming code of the project are contained in the 9 folders under the parent folder of  “code”.

## Folder 1: Weibo Blogger Account Spider
Python Code: Blogger Basic Information Scrapy With Weibo.ipynb
Weibo Makeup Blogger Spider: Crawl the basic information of makeup bloggers from Weibo, including blogger account name, ID, gender, region, tag, follows, fans and posts. By searching for Weibo users with 8 keywords, the program crawls 50 pages of bloggers’ information. 
The following three types of bloggers are removed:
- Duplicated bloggers;
- Bloggers with 0 follows, fans or posts;
- Marketing accounts (by using potential keywords contained in the name of MTKers);
- Bloggers unrelated with makeup (human labelling).
Append potential makeup bloggers (human labelling) and crawl the basic information of those bloggers.

## Folder 2: COSME Brand List Spider
1.Python Code: Brand Scrapy With Cosme.ipynb
Cosme Makeup Brand Spider: Crawl the brand names (both Chinese name and English name) listed on the COSME website, 3384 brands.
Normalize the brands names.
Append 50 medical beauty brands and domestic makeup brands, and drop duplicates.

## Folder 3: Weibo Post Spider:
1.Python Code: weibo.py
Weibo Post Spider: Detailed description is given by “README_Weibo Post Spider.md”. “requirements.txt” specifies the version of the package used. “config.json” initializes the spider, please specify the name of the text file including the uids of the bloggers  in this file.
Crawl the posts of the 2788bloggers for the year of 2019.   
2.Python Code: UID Split.ipynb
Split the union uid list given in the text file “uid.txt” to crawl the data separately.

## Folder 4: Weibo Post Omit Checker
1.Python Code: Bloggers Post Check.ipynb
Check the omitted posts in the crawling process, and then update the uid lists.

## Folder 5: Product Identifier and Tmall Spider
1.Python Code: Product Brand Identification in Post.ipynb
Product Name Identifier: Apply the customized dictionary of brand names, stop words, and end words. By constraining the word counts between the brand names and the end words, identify the product name in the post.   
2.Python Code: Product Scrapy With T-Mall.ipynb
T-Mall Product Information Spider: Crawl the product information from T-Mall, including product name posted on T-Mall, brand name, product price, popularity, product score, positive comment and negative comment.   
3.Python Code: Product Brand Re-Identification.ipynb
Product Name Validation: Check whether the product name crawled from T-Mall contain the brand name in the brand dictionary, if not, remove the corresponding product record.

## Folder 6: Weibo Brand Account Spider
1.Python Code: Brand Weibo Account.ipynb
Weibo Brand Account Spider: Impute missing brand names first, and then crawl the brand account, starting from Chinese names and then move on to English names. Record the crawled brand names and inaccessible brand names.   
2.Python Code: Brand Weibo Account Double-Check.ipynb
Check the missing brands omitted in the crawling process.

## Folder 7: Baidu Index Spider
1.Python Code: Baidu Index.ipynb
Baidu Index Spider: Search for daily Baidu index of a brand. If a brand has Baidu index for both its Chinese name and English name, take the maximum of the two as the integrated index. Detailed description is given by “README_Baidu Index.md”.    
2. Python Code: get_index.py, config.py
Define a class object for getting Baidu index, and configure for the spider.

## Folder 8: Weibo Supper Topic Spider 
1.Python Code: Super Topic.ipynb
Weibo Supper Topic Spider: Crawl the posts of a supper topic, the maximum post number is 5000. Detailed description is given by “README_Weibo Supper Topic Spider.md”.   
2.Python Code: seg.py
Text analytics and sentiment analysis for contents related to a supper topic on Weibo.   
3.Python Code: excelSave.py
Define a class object to execute statements on a batch of excel workbooks and sheets.

## Modelling
### Sub-Folder: Classifier
1.R Code: PCA.rmd
Perform principal component analysis on the number of likes, comments and reposts to obtain the loadings for PC1.   
2.Python Code: Data Pre-processing.ipynb
Perform the following procedures for data pre-processing: 
- Dump string variables;
- Remove lottery posts by using keywords (outliers with extremely large value of likes, comments and reposts);
- Convert un-structured data into structured data;
- Divide posts into 3 classes based upon the promotion performance by using K-Means algorithm, in which the response is the log value of the number of likes, the log value of PCA on the number of likes, comments and reposts, and the log value of the summation of the number of likes, comments and reposts.   
3.Python Code: Model Selection.ipynb
Model selection among multiple classifiers, including XGBoost, Gaussian Naïve Bayes, Logit Model, Random Forest, Balanced Bagging, Catboost. The optimal one with the highest kappa score is XGBoost.
Tune parameters for XGBoost, in terms of the depth of the tree and the number of estimator in each node of the tree.   
4.Python Code: XGBoost_Log Likes.ipynb, XGBoost_Log PCA.ipynb, XGBoost_Log Add. ipynb
Train XGBoost classifier with tuned parameters based upon the previous procedure, among which when using the log value of the summation of the number of likes, comments and reposts, the classifier has the best superior.
Make recommendation for Origin in terms of bloggers.
### Sub-Folder: Regression
1.R Code: Linear Regression.rmd
Apply linear regression to three types of response variable.   
2.Python Code: Random Forest-Regression.ipynb
Apply random forecast regression to three types of response variable.

## Folder 10: MySQL Connection
1.Python Code: MySQL Connection.ipynb
- Blogger List: save 'finalized_2788bloggers.csv' into MySQL Bloggers List 
- Post List: save 14 folders of post into MySQL Posts List.
- Old Brand List: save 'filtered_brands_df.csv' into MySQL Old Brand List
- Product-not-cleaned List: save 14 folders of product_name into MySQL Products-not-cleaned List.
- Product List: save 14 csv files in Cleaned_product_info into MySQL Products List
- New Brand List: save 'brand_data_final.csv' into MySQL Brands List

# Reference
1.Weibo-crawler: https://github.com/dataabc/weibo-crawler.git
2.weibo-topic-spyder: https://github.com/czy1999/weibo-topic-spyder.git
3.Baiduindex: https://github.com/longxiaofei/spider-BaiduIndex.git
