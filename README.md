# ADL
# Accumulation Distribution Line (ADL) Indicator Analysis and Trading Simulation  This Python script calculates and analyzes the Accumulation Distribution Line (ADL) indicator using sample stock price and volume data. It includes functionalities for plotting the ADL and simulating trading based on ADL signals.





```python
import pandas as pd
import matplotlib.pyplot as plt
from tti.indicators import AccumulationDistributionLine

# Sample data for demonstration
# The 'close' prices and 'volume' are essential for calculating the ADL.
data = {
    'close': [100, 102, 101, 103, 105, 104, 106, 108, 107, 109],
    'volume': [1000, 1500, 1200, 1800, 2000, 1600, 1900, 2200, 2100, 2500]
}

# Creating a DataFrame from sample data
df = pd.DataFrame(data)
# Setting the index to a date range for better visualization
df.index = pd.date_range(start='2021-01-01', periods=len(df), freq='D')

def calculate_adl(df):
    """Calculates the Accumulation Distribution Line (ADL) indicator.
    
    Args:
        df (DataFrame): The DataFrame containing stock price and volume data.

    Returns:
        AccumulationDistributionLine: An instance of the ADL indicator.
    """
    # Create an ADL indicator object with the input data
    adl_indicator = AccumulationDistributionLine(input_data=df)
    return adl_indicator

def plot_adl(adl_indicator):
    """Plots the ADL indicator.
    
    Args:
        adl_indicator (AccumulationDistributionLine): The ADL indicator to be plotted.
    """
    # Show the graphical representation of the ADL indicator
    adl_indicator.getTiGraph().show()

def simulate_trading(adl_indicator, df):
    """Simulates trading based on the ADL signals.
    
    Args:
        adl_indicator (AccumulationDistributionLine): The ADL indicator for trading simulation.
        df (DataFrame): The DataFrame containing stock price data.

    Returns:
        tuple: Simulation data, statistics, and the simulation graph.
    """
    # Execute trading simulation using ADL signals
    simulation_data, simulation_statistics, simulation_graph = \
        adl_indicator.getTiSimulation(
            close_values=df[['close']], 
            max_exposure=None,
            short_exposure_factor=1.5
        )
    return simulation_data, simulation_statistics, simulation_graph

def main():
    """Main function to execute the ADL calculation, plotting, and trading simulation."""
    # Calculate ADL
    adl_indicator = calculate_adl(df)
    
    # Display ADL data
    print('\nTechnical Indicator data:\n', adl_indicator.getTiData())
    
    # Get the most recent ADL value
    print('\nTechnical Indicator value at the last date:', adl_indicator.getTiValue())
    
    # Get and display trading signal
    print('\nTechnical Indicator signal:', adl_indicator.getTiSignal())
    
    # Plot ADL
    plot_adl(adl_indicator)
    
    # Simulate trading based on ADL
    simulation_data, simulation_statistics, simulation_graph = simulate_trading(adl_indicator, df)
    
    # Display simulation results
    print('\nSimulation Data:\n', simulation_data)
    print('\nSimulation Statistics:\n', simulation_statistics)
    
    # Show simulation graph
    simulation_graph.show()

if __name__ == "__main__":
    main()
```

### Explanation:
1. **Sample Data:** A dictionary containing closing prices and volumes for 10 trading days is created and then converted to a DataFrame.

2. **Calculate ADL (calculate_adl):** This function calculates an instance of the `AccumulationDistributionLine` class using the input data and returns it.

3. **Plot ADL (plot_adl):** This function displays the ADL graph.

4. **Simulate Trading (simulate_trading):** This function simulates trading based on the ADL signals and returns the data and statistics.

5. **Main Function (main):** This function manages all steps, including ADL calculation, displaying data, plotting graphs, and simulating trades.

You can place this code in your GitHub repository and easily expand upon it.
