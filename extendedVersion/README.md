# Here are the options for applying the model from the original article with the data obtained from the vulnerability scanner
In our case, we used a Clair scanner. Due to the fact that Clair finds a huge number of vulnerabilities in one docker container - we have presented 3 options for submitting data to the model

## The first version provides the following algorithm:
From the data received by the scanner, we get a list of vulnerabilities, which are distributed according to severity. From this list we take the first nonzero number of vulnerabilities. This number will be our number of machines on the network. Let's imagine that an attacker cannot crack each of these vulnerabilities, since they are inherently different - this will give us the right to assume that some of them will be feasible for him, while others will not. In this case, we will get the same data set for transferring to the model.

## Second version

Minor changes have been made to SecondVersion - we similarly get the first non-zero number in the list - `n`. Then we randomly generate a number in the range from `0` to `100 - n`. As a result, the number n will be the number of vulnerable machines in the network, and the second number represents the "healthy" machines.

## Third version

Here we create a network of vulnerable and healthy docker containers. we scan each of them and place the reports in a specific folder. As it turned out in practice, every container we tested had some kind of vulnerability. Therefore, we have replaced some of the reports with those that do not contain the WoolNeed fields. Then we go through these reports and get data that can be sent to the model. 
