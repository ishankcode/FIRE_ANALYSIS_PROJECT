# FIRE_ANALYSIS_PROJECT

As a student consultant as part of the STAT-683 Data Science Capstpone Course Worked with Texas A&M Forese Services to think of out of box ideas utliiziang the massive data available on past fire records in state of Texas, USA to improve fire-respone time.

-----

<ins>SKILLS & TOOLS USED</ins>
- Python Libraries: Numpy, Pandas, Daex, SQLALCHEMY, Gurobi Solver, Pycaret, Folium, Seaborn, Matplotlib
- SQL
- Tableau
- Microsoft Excel
- Linear Programming, Gurobi Solver

-----
                                                                                  
| Dataset_NAM              | DataSize     | Imp Features                                                                 |Dataset_Link                        |
| :---:                    | :---:        | :---:                                                                        |:---:                               |
| Fire_Records (1992-2015) | 1.4M+        | Location, Area, Cause, Duration, DiscoveryDate & Time, Contained Date & Time |https://shorturl.at/clF23           |
| Weather_Data (1985-2015) | 2.8M+ Yearly | Hourly Data - Temperature, Windspeed,Humidity                                |https://mesonet.agron.iastate.edu/request/download.phtml?%20network=TX_ASOS        |
| Fire_Stations (Current)  | 1,840        | Location, Resources (Personals Volunteers & Paid)                            |Multiples_Files (recived from TFS)  |
| Fire_Weather_Data (2022))| 4,500        | Temperature, Windspeed, Humidity etc ,(Testing Purpose for IWDA)             |[https://shorturl.at/clF23 ]        |

As student Consultant I worked in teams of 2 and had weekly meetings with TFS Team as well as the project mentor.The point of meetings was to update the team regarding our progress as well as discuss new ideas that can be implemented now or in the future which will be helpful for forest inventory team as well as fire-response team. 

<ins>The Projects is divided in 4 main tasks:</ins>

- Data Collection, Data Exploration, Data Engineering
- Developing Machine Learning Modelsm (To predict fire-size class based on the weather properties at time of ignition)
- Time-Series Analysis (Done Quickly to demonstrate thr capabilities of this type of Analysis to TFS Team)
- Optimization Model (Developing model to identify optimum location of fire-stations)

<ins>Part 1 : Data Engineering</ins>
1. This was definately the toughest part of project and took Maximum Time because of lack of Domain Knowledge as the Forest invetory data (not mentioned here) was\ so large with around 1000+ page documentation that was not updated frequently. And someone new it was definately challenging but we still developed some insights\ that were shared to the TFS team seperatley.
2. Next biggest task was that for our classification model we wanted the weather data that was at that particular location and at that partical time. For that various options were explored such as Inverse Distance Weighted approach, Kridging, Baycentric Coordinate System method (Did not work out very well Because most data poiints were existing outside any possible triangles)
3. third biggest problem was the size of data, we had almost 1.4M+ fire recorded for past 25 years in state of Texas and to identify the correct weather properies (data recorded almost thrice hourly) was approx 2.8M*25 so had to optimize the python code a lot to reduce the computation time. Used advanced python features and libraies like Numpy, Pandas, DAEX and some data structures like Dictionaries to reduce computation time. Went from taking approx a days time to less than 1 hour.

<ins>Machine Learning</ins>
1. Because this was a course project and we had only maximum 3.5 months in time in total and lot of time was used in data engineering step so we decided to use Pycaret to develop Machine learning models for 2 reasons as it will help in developing models quickly and secondly we will get the opprtunity to explore new cool library.
2. Fearture engineering - Dropped Irrelevant data, Performed Label Encoding & One-hot encoding, Normalization, Binning of Numeric variables etc
3. The main problem faced during this was the class Imbalance, because our target variable was fire-size class that among the 7 class categories:
    - fire_size_class "G" : only 236 records out of 1.4M
    - fire_size_class "F" : only 792 records out of 1.4M
    - fire_size_class "B" : 90,462 records capturing almost 65% of data
To handle the class imbalance issues various methods like SMOTE, Assigning Class Weights, Random over Sampling were used to improve the datasets.
4. Finally leveraged the pycaret library and created numerous models that we belive would be good fit for our model but we encoutered <ins>Accuracy Paradox</ins>
as even though model of accuracy was high (because of class imbalance issue) and thus tuned the model to optimize precision and recall
5. Used Strarified cross validation and identified random forest Bagging model to be the best.
This part require a lot more work as these are prelimanry resukts and can be improved a lot further( also did some work in connecting with data with forest propties that will provide new features)

<ins>Time Series Analysis</ins>
1. Perfomed Fire Size time series analysis aggregated to monthly data, hypertuned model by grid search. 
2. Perfomed Fire Frequency time series analysis aggregated to monthly data, hypertuned model by grid search. 

<ins>Optimization model</ins>
1. Explored Voronoi diagram for state of Texas, 1840 fire station to understand approximately how much area each firestation has to cover.We onserved that west texas has very less fire-stations this might be because of lack of forest resulting in less devastating fires (supported by data)
2. Discretized the state of Texas into small grids of 5*5 km^2.
3. General rule is that all fires should be responded within 6 mins, so in our data we removed all fires that would have been responded in less than 8 mins based on current number of firestations. Assigned a grid_id to each remaining fire_record.
4. Assumption was made that any fire_station is at center of the grid(for ease of calculation), based on this for each grid we identified number of grids that station can repond to within a specefic time. Based on this criteria we used the developed optimization model.
5. Key Results - developed a [tableau dashboard](https://public.tableau.com/app/profile/ishank.gupta1043/viz/Unattendedfireswithinsafetime/Dashboard1?publish=yes)
for prsenting our results. Results are summarized in table below as well:
![image](https://github.com/ishankcode/FIRE_ANALYSIS_PROJECT/assets/66678343/0fd2e669-6ceb-4cf6-93f6-b8d2dff80fe3)



