##Code Book for the Data Cleaning project

This code book describes the tidy dataset created by the run_analysis.R script. 

The dataset.txt is the tidy data set derived from step 5 by calculating the average of each variable for each activity and each subject

##The tidy dataset.txt

subject - suject is the person who carried the experiments - valid values are integer and ranges from 1 to 30. 
This column is orginally from subject_train.txt/subject_test.txt dataset                      

activity - the activity carried out by the subject. There are six activities and they are 

WALKING

WALKING_UPSTAIRS

WALKING_DOWNSTAIRS

SITTING

STANDING

LAYING

These values are originally defined in activity_labels.txt and column values are column merged from y_test.txt/y_train.txt

Rest of the columns are extracted from the orignal dataset X_test.txt/X_train.txt by dropping all the columns 
which are not having mean or std and they are transformed by removing '-','()' and lowering the case

But the values of these columns are the average of each variable for each activity and each subject. 
The mean function is applied for the same to get the average.
There are 180 rows in the dataset. That is 6 activities * 30 subjects = 180 rows. 
All these column values are numeric.

The renamed columns are

tbodyaccmeanx 
tbodyaccmeany               
tbodyaccmeanz            
tbodyaccstdx                
tbodyaccstdy                 
tbodyaccstdz                
tgravityaccmeanx             
tgravityaccmeany            
tgravityaccmeanz            
tgravityaccstdx             
tgravityaccstdy             
tgravityaccstdz             
tbodyaccjerkmeanx           
tbodyaccjerkmeany          
tbodyaccjerkmeanz           
tbodyaccjerkstdx            
tbodyaccjerkstdy            
tbodyaccjerkstdz            
tbodygyromeanx              
tbodygyromeany              
tbodygyromeanz              
tbodygyrostdx               
tbodygyrostdy                
tbodygyrostdz               
tbodygyrojerkmeanx          
tbodygyrojerkmeany          
tbodygyrojerkmeanz           
tbodygyrojerkstdx           
tbodygyrojerkstdy            
tbodygyrojerkstdz           
tbodyaccmagmean             
tbodyaccmagstd              
tgravityaccmagmean 
tgravityaccmagstd           
tbodyaccjerkmagmean 
tbodyaccjerkmagstd          
tbodygyromagmean            
tbodygyromagstd             
tbodygyrojerkmagmean 
tbodygyrojerkmagstd         
fbodyaccmeanx            
fbodyaccmeany               
fbodyaccmeanz               
fbodyaccstdx                
fbodyaccstd                 
fbodyaccstdz                
fbodyaccmeanfreqx          
fbodyaccmeanfreqy           
fbodyaccmeanfreqz            
fbodyaccjerkmeanx           
fbodyaccjerkmeany            
fbodyaccjerkmeanz           
fbodyaccjerkstdx 
fbodyaccjerkstdy            
fbodyaccjerkstdz             
fbodyaccjerkmeanfreqx       
fbodyaccjerkmeanfreqy        
fbodyaccjerkmeanfreqz 
fbodygyromeanx               
fbodygyromeany              
fbodygyromeanz               
fbodygyrostdx               
fbodygyrostdy                
fbodygyrostdz           
fbodygyromeanfreqx           
fbodygyromeanfreqy          
fbodygyromeanfreqz           
fbodyaccmagmean             
fbodyaccmagstd           
fbodyaccmagmeanfreq      
fbodybodyaccjerkmagmean      
fbodybodyaccjerkmagstd  
fbodybodyaccjerkmagmeanfreq 
fbodybodygyromagmean        
fbodybodygyromagstd     
fbodybodygyromagmeanfreq     
fbodybodygyrojerkmagmean    
fbodybodygyrojerkmagstd 
fbodybodygyrojerkmagmeanfreq

