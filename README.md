

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
