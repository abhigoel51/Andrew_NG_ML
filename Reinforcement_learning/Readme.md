# Reinforcement Learning

**What is it ?**  
Basically we are trying to calculate the reward for moving left or right.  
We take in the consideration the number of steps needed to get the award, this is taken into account with discount factor.

<img width="1331" height="630" alt="image" src="https://github.com/user-attachments/assets/d649c3e2-dcd4-49fe-b1a2-ea3746f33382" />

**What is the importance of Discount Factor ?**  

Let's Consider a Scenario, i am on state 5 with discount factor = 0.3.  

**Calculating Reward in both directions -**   

For moving right - 0 +(0.3)*4 = 12  
For moving left - 0 + 0.3*0 + (0.3^2)*0 + (0.3^3)*0 + (0.3^4)*100 = 8.1  

The reward is higher for moving right. So the discount factor decides, whether to wait for the higher reward or move to closest reward. If we increase discount factor to 0.9, for right - 36 , for left - 65.61 

## State-action value function

**Q(s,a)** - Calculates the reward for every state for a particular action (left or right in example).  

Below is the example when discount factor = 0.9, we calculate all possible **Q** for all states.  
And then we will choose the Max value of both and direction, as shown below.

<img width="1253" height="208" alt="image" src="https://github.com/user-attachments/assets/1a524033-8223-415e-bbc9-bca716f648b8" />

<img width="1033" height="160" alt="image" src="https://github.com/user-attachments/assets/b1a09930-20d1-4135-b5a3-27e3bb79d44e" />

Another example when Discount factor is 0.3, notice how direction are different for optimal policy  

<img width="1035" height="323" alt="image" src="https://github.com/user-attachments/assets/7b18e97b-7647-4658-8e6e-a8a3b5f5203b" />

## Bellman Equation

<img width="1468" height="750" alt="image" src="https://github.com/user-attachments/assets/acd7afe7-5237-4103-ac3a-23489e0d6acb" />

<img width="588" height="200" alt="image" src="https://github.com/user-attachments/assets/102e52ed-ed0c-4ff6-9b8a-318a9683761e" />

### Stochastic 

When we want to move the robot in a certain direction but chances of robot moving in the same direction may be not be 100%, may be due to external factors or any other reason. For .e.g Robot is trying to move on wet space, which causes it to slip and is not able to move in the intented direction.

So to solve the problem we take the **average of next state in Bellman equation** 

Considering discount factor as 0.3 as above and mistep_pob as 0.2, earlier it was 0.

<img width="1036" height="228" alt="image" src="https://github.com/user-attachments/assets/49f205f5-5755-49a5-a7a3-92e8f2529722" />

Comparing it with previous optimal policy diagram, the reward for moving in a certain direction has decreased.
