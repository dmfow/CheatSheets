## Simple

#### Simple line plot
```python
plt.figure()
plt.plot(df["dowJones"], color='pink') # The line color (and many other properties) can be customized
plt.xlabel("Time index")
plt.ylabel("Return")
plt.show()
```

#### Simple scatterplot with legends
```python
plt.figure()
plt.xlabel("Volatility")
plt.ylabel("Return")

# Plot stock values as scatter (eg std and return in this example)
plt.scatter(df_stocks_std.values, df_stocks_returns.values, color='black', label='Nasdaq')

# Plot a line, as dots
plt.plot(myLine_std, myLine_return, color='green', linestyle='--', label='Some line')

# Highlight a point '*' marker
plt.scatter(pointStdValue, pointReturnValue, color='red', marker='*', s=100, label='My special point')

plt.legend()
plt.show()

# In the plt statement
  # linestyle = 'solid'            # https://matplotlib.org/stable/gallery/lines_bars_and_markers/linestyles.html
  # marker = 'o',                  # https://matplotlib.org/stable/api/markers_api.html
  # markerfacecolor = 'red'
  # markersize = 12

```


## Multiple

#### Plot line with multiple graphs
```python
fig, ((ax1, ax2),(ax3, ax4)) = plt.subplots(2, 2, figsize=(10, 3))

ax1.set_title("Dow Jones")
ax1.set_xlabel("Time")
ax1.set_ylabel("Return")
ax1.set_ylim([0, 20000])

ax2.set_title("S&P 500")
ax2.set_xlabel("Time")
ax2.set_ylabel("Return")
ax2.set_ylim([0, 20000])

ax3.set_title("Nasdaq")
ax3.set_xlabel("Time")
ax3.set_ylabel("Return")
ax3.set_ylim([0, 20000])

ax1.tick_params(axis='x', labelrotation=90)
ax2.tick_params(axis='x', labelrotation=90)
ax3.tick_params(axis='x', labelrotation=90)

ax1.plot(df["dowJones"], color='red') # Line color
ax2.plot(df["sp500"], color='blue')
ax3.plot(df["nasdaq"], color='green')

plt.tight_layout()

plt.show()
```

