
## Download and Write Files directly from URL's into LOCAL Machine

    from urllib.request import urlretrieve
    from urllib.error import HTTPError
    
    urlretrieve(imagepath+key_append, file_name)

### BASE64 Image crop and Extraction with bounding Box
def getBase64(image1,bbox,img_string):

    im = Image.open(BytesIO(image1)).convert('RGB')
    np_image = np.array(im)

    # Convert RGB to BGR
    crop_img = np_image[ bbox[3] :bbox[4],bbox[1] :bbox[2]]
    im_cr = Image.fromarray(crop_img)
    
    # Buffer array to store Image in memory
    output = BytesIO()
    saved = im_cr.save(output, format='JPEG')
    encoded_string = base64.b64encode(output.getvalue())

    return encoded_string


## SQL With Pandas

#### Where clause condition: 
        job_code = 'LE130846' 
        
        # Variable foramtting
        job_code = """'""" +job_code + """'"""


        sql_query = ("select FrontCameraPath  FROM [WeighmentDB].[dbo].[Weighment_Detail] " +
            " WHERE CreatedDatetime > '2019-12-23 00:00:00' "+
            "  AND AIVehicleNo != '_NOPLATE_' " +
            " AND ANPRInfo != ''  and jobcode = " +(job_code) )
        sql_query



## Working with Directories

#### Creating Directories
        import os
        def create_directory(job_code):
            try:
                os.mkdir(job_code)
                os.mkdir(job_code+'/NoPlate/')
                os.mkdir(job_code+'/CorrectPlate/')
                os.mkdir(job_code+'/IncorrectPlate/')

            except OSError:
                print ("Creation of the directory %s failed!" % job_code)

            else:
                print ("Successfully created the directory %s " % job_code)
        create_directory('LE120450')


#### removing Directories
        import shutil
        try :
            shutil.rmtree(job_code)
            print(job_code, " Directory Already exists. Dropping and Recreating ", job_code)


except:
    print("Creating Directory: ", job_code)
    extract_all_images(job_code)


## Custom aggregate Function for Resample/ Group by:
        # agg func
        def hour(series):
          per = 0
          for i in series:
            if i==1:
              per+=1
          return per*30/(60*60)
        
        # function call
        df2_Clean['EngineStatus'].resample('1d').agg(hour)
        
        or
        # using lambda function
        df2_Clean['EngineStatus'].resample('1d').agg(lambda x: sum(x)*30/3600)

## Code to plot two different axis on Same Plot:

    fig, ax1 = plt.subplots(figsize=(22,8))

    df2_Clean.EngineStatus.plot(title = "Engine Status",color = 'orange')
    df2_Clean['EngineStatus'].resample('1d').sum().plot(title = "EngineStatus Daily Average",  color = 'Blue')
    mean_value_EngineStatus =df2_Clean['EngineStatus'].resample('1d').sum().mean()

    plt.axhline(y=mean_value_EngineStatus, color='black', linestyle='--')

    #legend
    label =('EngineStatus' ,'Daily Avergae EngineStatus' , '3 month average EngineStatus')
    plt.legend(loc = 'upper left', labels = label )

    plt.ylabel("EngineStatus")


    ax2 = ax1.twinx()  # instantiate a second axes that shares the same x-axis

    color = 'tab:Orange'
    ax2.set_ylabel('ON/OFF', color=color)  # we already handled the x-label with ax1
    ax2.plot(df2_Clean.EngineStatus, color=color)
    ax2.tick_params(axis='y', labelcolor=color)

    fig.tight_layout()  # otherwise the right y-label is slightly clipped

    #Label X-Axis
    plt.xlabel("Time")

    #Show plot
    plt.show()

### Stacked Histogram plot

    sns.set_style("darkgrid")
    plt.set_cmap('jet')
    plt.figure(figsize=(15, 6))
    _, bins, _ = plt.hist([machines.loc[machines['model'] == 'model1', 'age'],
                           machines.loc[machines['model'] == 'model2', 'age'],
                           machines.loc[machines['model'] == 'model3', 'age'],
                           machines.loc[machines['model'] == 'model4', 'age']],
                           20, stacked=True, label=['model1', 'model2', 'model3', 'model4'])
    plt.xlabel('Age (yrs)')
    plt.ylabel('Count')
    plt.legend()
    plt.title("Count of Each Machine in each Age Category")
    plt.show()

### Source Code to plot two different axis on Same Plot:

        import numpy as np
        import matplotlib.pyplot as plt

        # Create some mock data
        t = np.arange(0.01, 10.0, 0.01)
        data1 = np.exp(t)
        data2 = np.sin(2 * np.pi * t)

        fig, ax1 = plt.subplots()

        color = 'tab:red'
        ax1.set_xlabel('time (s)')
        ax1.set_ylabel('exp', color=color)
        ax1.plot(t, data1, color=color)
        ax1.tick_params(axis='y', labelcolor=color)

        ax2 = ax1.twinx()  # instantiate a second axes that shares the same x-axis

        color = 'tab:blue'
        ax2.set_ylabel('sin', color=color)  # we already handled the x-label with ax1
        ax2.plot(t, data2, color=color)
        ax2.tick_params(axis='y', labelcolor=color)

        fig.tight_layout()  # otherwise the right y-label is slightly clipped
        plt.show()
        
        
### Custom Legend 
        plt.legend(loc = 'upper left', labels = label , facecolor= 'grey' , framealpha = 0.5, fontsize = 'large', bbox_to_anchor = [0.8,0.1, 1, 1])
