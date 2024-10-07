# Reputation System

Upon successfully completing a purchase or sale of sats, Mostro will ask you to rate your counterparty, and your counterparty will also rate you. The reputation system uses a 5-star rating scale, where 1 star represents the lowest rating and 5 stars the highest, allowing you to evaluate the transaction experience.

Reputation in Mostro is calculated iteratively, combining the mean and standard deviation of ratings and successful transactions. This means that during your first transactions, even if you receive maximum ratings, your initial reputation will not be very high; instead, it will progressively increase as you accumulate more successful transactions with good evaluations.   
This calculation is based on: [https://math.stackexchange.com/questions/2148877/iterative-calculation-of-mean-and-standard-deviation](https://math.stackexchange.com/questions/2148877/iterative-calculation-of-mean-and-standard-deviation).
