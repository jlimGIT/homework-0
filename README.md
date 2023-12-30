# homework-0
My first GitHub repo
import requests
import pandas as pd

class InvestmentProfile:
    def __init__(self, objectives, risk_tolerance, time_horizon, liquidity_needs, tax_considerations):
        self.objectives = objectives
        self.risk_tolerance = risk_tolerance
        self.time_horizon = time_horizon
        self.liquidity_needs = liquidity_needs
        self.tax_considerations = tax_considerations

def determine_asset_allocation(profile):
    # Advanced logic based on multiple factors
    if profile.risk_tolerance == 'High':
        equities = 70
    elif profile.risk_tolerance == 'Medium':
        equities = 50
    else:
        equities = 30

    if profile.time_horizon > 10:
        equities += 10

    bonds = 100 - equities - 10  # Keeping a fixed 10% in alternatives
    return {'Equities': equities, 'Bonds': bonds, 'Alternatives': 10}

def fetch_fund_data():
    # Placeholder for fetching fund data from an external source
    # In practice, this might involve API calls to financial data providers
    url = "https://api.example.com/funds"  # Example URL
    response = requests.get(url)
    data = response.json()
    return pd.DataFrame(data)

def select_funds(asset_allocation, fund_data):
    # Advanced selection logic based on fund performance, expense ratio, etc.
    selected_funds = {}
    for asset_class in asset_allocation:
        if asset_allocation[asset_class] > 0:
            class_funds = fund_data[fund_data['AssetClass'] == asset_class]
            # Example: Select top 2 funds based on performance
            top_funds = class_funds.sort_values(by='Performance', ascending=False).head(2)
            selected_funds[asset_class] = list(top_funds['FundName'])
    return selected_funds

def generate_recommendation(ips, fund_data):
    profile = InvestmentProfile(**ips)
    asset_allocation = determine_asset_allocation(profile)
    recommended_funds = select_funds(asset_allocation, fund_data)
    return asset_allocation, recommended_funds

# Load or fetch fund data
fund_data = fetch_fund_data()

# Example IPS input
ips_example = {
    'objectives': 'Growth',
    'risk_tolerance': 'Medium',
    'time_horizon': 15,
    'liquidity_needs': 'Low',
    'tax_considerations': 'Standard'
}

# Generate recommendation
allocation, recommendation = generate_recommendation(ips_example, fund_data)
print("Recommended Asset Allocation:", allocation)
print("Recommended Funds:", recommendation)