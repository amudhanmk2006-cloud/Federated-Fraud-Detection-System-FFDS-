print("===== SMART FRAUD DETECTION SYSTEM =====")

# Get customer details from user
name = input("Enter customer name: ")
amount = float(input("Enter transaction amount: "))
transactions = int(input("Enter number of transactions in 24 hours: "))
unusual_location = input("Is the location unusual? (yes/no): ").lower()
hour = int(input("Enter transaction hour (0-23): "))
rapid_transfers = int(input("Enter number of rapid transfers: "))
usual_amount = float(input("Enter usual transaction amount: "))
failed_pins = int(input("Enter failed PIN attempts: "))

# Convert location into True or False
unusual_location = unusual_location == "yes"

# BANK A - Transaction Activity
if amount > 50000 or transactions >= 5 or rapid_transfers >= 5:
    bank_a = "FRAUD"
else:
    bank_a = "LEGITIMATE"

# BANK B - Location and Timing
if unusual_location or 0 <= hour <= 5:
    bank_b = "FRAUD"
else:
    bank_b = "LEGITIMATE"

# BANK C - Customer Behaviour
if amount > 3 * usual_amount or failed_pins >= 3:
    bank_c = "FRAUD"
else:
    bank_c = "LEGITIMATE"

# Display bank predictions
print("\n===== BANK PREDICTIONS =====")
print("Bank A:", bank_a)
print("Bank B:", bank_b)
print("Bank C:", bank_c)

# Calculate risk score
risk_score = 0

if amount > 50000:
    risk_score += 2

if transactions >= 5:
    risk_score += 2

if unusual_location:
    risk_score += 2

if 0 <= hour <= 5:
    risk_score += 1

if rapid_transfers >= 5:
    risk_score += 2

if amount > 3 * usual_amount:
    risk_score += 2

if failed_pins >= 3:
    risk_score += 3

# Find risk level
if risk_score <= 2:
    risk_level = "LOW"
elif risk_score <= 5:
    risk_level = "MEDIUM"
else:
    risk_level = "HIGH"

# Final decision using majority voting
fraud_votes = [bank_a, bank_b, bank_c].count("FRAUD")

print("\n===== FINAL ANALYSIS =====")
print("Customer Name:", name)
print("Total Risk Score:", risk_score)
print("Risk Level:", risk_level)
print("Fraud Votes:", fraud_votes, "out of 3")

if fraud_votes >= 2:
    print("RESULT: FRAUD DETECTED")
else:
    print("RESULT: TRANSACTION IS LEGITIMATE")

print("\n===== ANALYSIS COMPLETED =====")
