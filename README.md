- 👋 Hi, I’m @Siatek98
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Siatek98/Siatek98 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import datetime

def psi_numerator(y, swapRate, accrualFactorLiborRate):
    try:
        tau = accrualFactorLiborRate
        num_term1 = (swapRate * tau) / (1 + tau * y)
        num_term2 = 1 / (1 + tau * y)
        return num_term1 + num_term2 - 1
    except Exception as e:
        return f"Error-handling: unexpected error occurred - {e}"

def psi(y, swapRate, accrualFactorLiborRate, paymentDate, fixingDate, dayCount, time_fraction_fixing_paymentdate):
    try:
        if paymentDate <= fixingDate:
            return (paymentDate - fixingDate).days  # Zwrot różnicy w dniach

        tau = accrualFactorLiborRate
        timeFractionFixingToPayment = ((paymentDate - fixingDate).days / dayCount) * time_fraction_fixing_paymentdate

        num = psi_numerator(y, swapRate, accrualFactorLiborRate)
        denom = 1 / (1 + timeFractionFixingToPayment * y)

        return num / denom
    except Exception as e:
        return f"Error-handling: unexpected error occurred - {e}"

# Przykład użycia:
paymentDate = datetime.date(2050, 7, 15)
fixingDate = datetime.date(2050, 7, 8)
y = 0.05
swapRate = 0.02
accrualFactorLiborRate = 0.25
dayCount = 360
time_fraction_fixing_paymentdate = 1.0

result = psi(y, swapRate, accrualFactorLiborRate, paymentDate, fixingDate, dayCount, time_fraction_fixing_paymentdate)
print(result)
