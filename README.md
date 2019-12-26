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

    `fig, ax1 = plt.subplots(figsize=(22,8))

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
    plt.show()`



### Source Code to plot two different axis on Same Plot:

        `import numpy as np
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
        `
