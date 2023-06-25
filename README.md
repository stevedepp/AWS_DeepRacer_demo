# AWS DeepRacer  

TGIF project: What can I learn about AWS DR in one day?

Please click the video to hear sound or follow along with the slides and transcript below the video.
(In this case, I think the demo video is better than the transcript / slides below.)

<video src="https://user-images.githubusercontent.com/38410965/111689560-92d9ee00-8802-11eb-9406-4075edc93d90.mp4" autoplay controls loop muted style="max-width: 730px;">
</video>

#

> Thank you for tuning into my video.  What you’re looking at over on the right hand side is a simple AWS racer with one eye, no LIDAR, moving at slow speeds, around a moderately complex track, trained by a simple shallow neural net.  The red line, which just ticked down from 100%, was showing that the car was able to complete 100% of the track during evaluation. The blue line was showing that the car was able to achieve 55% of the course during training. 

### 1. TGIF

**Steve Depp**     
**462**     

**AWS Deep Racer**     

Time trials = alone on track     
	
No obstacles     
——>	no depth perception needed     
	
No other racers     
——>	no LIDAR needed     
——> 	simplest car with only 1 camera “Popeye”     
——>	fewer action-state pairs      
——> 	simpler model & speedier training     

<img width="911" alt="Front facing" src="https://user-images.githubusercontent.com/38410965/116015307-bb75b480-a606-11eb-8fc0-264af4874ec4.png">

#

> The difference between the red and blue line is also the difference in completion as the model as the model explores in training, and is greedy about its choices in evaluation.  It’s only going for sure things in evaluation, and that’s why the red line is well above the blue line.  

### 2. Training metrics show value of exploration —> generalization     

**Seen in 2 ways:**     

<img width="597" alt="image" src="https://user-images.githubusercontent.com/38410965/116015445-40f96480-a607-11eb-85b2-44d1f18d66c7.png">

#

> So, I found, you know, in doing this, (it was really easy), that the AWS DeepRacer is a great place to learn or apply reinforcement learning.  It has all the ingredients that you need: so, environment, state, agent, actions and rewards.  So, we’ve discussed the car already, and briefly touched upon the environment, but, you know, with more turns, obstacles, other racers, narrower roads, longer roads, you have more state accommodations to deal with, more complexities. So, you have to have a more complex model, which requires more time and money to run.  So, I ran my model about 2 hours, but if you had to do that over and over again, it could get kind of expensive. 

### 3. Great place to learn RL     

- [x] **RL ingredients**     


		environment —> states    —> agent —> actions          —> rewards     
		race track  —> race type —> car   —> speed & steering —> points     

- [x] **Agent = car**     

- [x] **Environment = track** 

		turns      
		obstacles      
		other racers     
		narrower roads     
		longer roads (bigger batch size)     
		——> more state combinations      
		——> more complex agent needed     
		= more complex model     
		= more time & money     

<img width="720" alt="The 2019 DeepRacer" src="https://user-images.githubusercontent.com/38410965/116015794-95e9aa80-a608-11eb-800b-a43b6f0e142d.png">

#

> So, my objective for, you know this project was to play around with AWS a bit, to apply reinforcement learning concepts, to build a model, and to look under the hood of AWS and the model itself.   AWS makes easy to do this in just really, you know, 5 steps.  

![images](https://user-images.githubusercontent.com/38410965/116015812-a4d05d00-a608-11eb-99f8-830b9d601912.jpeg)

### 4. Objective:     

- Play with AWS console      
- Apply RL Concepts      
- Build a time trial model     
- Under the hood     

**Novice with limited budget:**     

- environment = race track with gentle turns	     
- race type = time trial = alone on track     
- car = one headlight + no mirrors     
- actions = slow is 1m/s & steady has fewer steering clicks     
- rewards = not too slow, stay in middle, don’t turn too much     

—> quickly training model     

**5 steps to submitting a model to the April time trials**     

**Later:**     

- better robot hardware     
  - head to head      
  - object avoidance     
  - object recognition     
- better understanding      
  - bootcamp videos (21 total)     
    - https://www.aws.training/Details/eLearning?id=32143     
  - AWS Training and Certification team:     
    - https://www.aws.training/Details/eLearning?id=32143     

#

> Step zero is getting hooked up to AWS.  They make it real easy. I already had an account there.  The IAM roles were already set up, but it was interesting to see what the IAM roles are; they’re listed there.  The resources that are necessary: there are 5 sets of resources there, and they’re well documented.   So, that was also very interesting to see.  

<img width="693" alt="To get you set up, AWS DeepRacer needs to create account r" src="https://user-images.githubusercontent.com/38410965/116016060-6d15e500-a609-11eb-9d48-507e79328320.png">

### Step 0 = 5 minutes	     
		
**IAM roles defined in pop out if needed**	     
- AWS DR requires      
- Service Role —> resources & make calls     
  - Maker Role —> SageMaker manage resources     
  - RoboMaker Access Role —> RoboMaker manage resources     
  - Lambda Access Role —> Lambda function calls resources     
  - CloudFormation Access Role —> create/manage needed stacks     
	
**AWS Resources**      
- CloudFormation stack     
  - Learn about [AWS CloudFormation](https://aws.amazon.com/cloudformation/)    
- S3 bucket     
  - model configurations     
  - training output     
  - virtual circuit logs     
  - Learn about [AWS S3](https://aws.amazon.com/s3/)     
  - AWS Lambda      
  - test reward function —> training model     
  - Learn about [AWS Lambda](https://aws.amazon.com/lambda/)     
- AWS RoboMaker / SageMaker     
  - SageMaker training job     
  - RoboMaker simulation     
  - inside VPC (Virtual Private Cloud)     
  - exchange data via S3     
- AWS RoboMaker simulation application     
  - virtual AWS DR representation      
  - onto     
  - virtual representation of track     
  - using rigid body physics simulator     
  - —> predictions of real world behavior     

#

> Step one is, you know, learning reinforcement learning basics, and they walk you through this in several really concise slides.  


### Step 1 = Learn RL basics 

RL drives the DR     
Know RL —> create / optimize model that drives your car —> win     

<img width="1052" alt="What is reinforcement learning" src="https://user-images.githubusercontent.com/38410965/116016426-9420e680-a60a-11eb-8345-4bb12ec7dff7.png">

<img width="473" alt="In reinforcement learning, an agent interacts with an" src="https://user-images.githubusercontent.com/38410965/116016436-997e3100-a60a-11eb-87ee-a94a13f1e25b.png">

#

> There’s the agent.  

### Step 1.1

<img width="1041" alt="The agent simulates the AWS DeepRacer vehicle in the" src="https://user-images.githubusercontent.com/38410965/116016446-a13dd580-a60a-11eb-9a78-348d2373ef57.png">

#

> There’s the environment.  

### Step 1.2

<img width="1040" alt="Environment" src="https://user-images.githubusercontent.com/38410965/116016455-a8fd7a00-a60a-11eb-928d-a27ab70f6ce1.png">

**So easy: Will these become household words?**
- agent
- environment 
- action			
- state 			
- reward

#
 
> There’s the action. 

### Step 1.3

Action	= agents moves = steering angle + speed

<img width="1034" alt="Steering" src="https://user-images.githubusercontent.com/38410965/116016484-bd417700-a60a-11eb-8cde-3cb8cdde8be0.png">

#

> The states.  

### Step 1.4

state = camera feed + LIDAR + boxes on tarmac

<img width="1046" alt="Environment" src="https://user-images.githubusercontent.com/38410965/116016501-c92d3900-a60a-11eb-810b-c7f26ffc70d5.png">

#

> And the rewards. 

### Step 1.5 

Reward 
- environmental feedback to agent per action and state
- defined by reward function 

<img width="1034" alt="The reward is the score given as feedback to the agent when it" src="https://user-images.githubusercontent.com/38410965/116016541-eb26bb80-a60a-11eb-9e08-2e432882c782.png">

#

> So, in step two, you create a model. So, we’ve already sort of gone through the car and the environment.  For rewards, I grafted together a couple different rewards snippets that they already had, and in the end, it ended up so that the car would not go too slow, it would not make too many turns, sharp turns, and would always remain in the center of the road.  

### Step 2 

**Create Model**     
- [x] Agent = car     
- [x] Environment = track     
- [ ] Reward function:     

Give the dog a bone …     

<img width="209" alt="Position on track" src="https://user-images.githubusercontent.com/38410965/116016575-05f93000-a60b-11eb-9655-5bca7dddd8bd.png">

**Grafted 2 different snippets:**     

Pseudocode:     

def reward_function:     

		Distance from center:          
			0.10 meter —> 1.00 reward     
			0.25 meter —> 0.50 reward     
			0.50 meter —> 0.10 reward     
			#^$%@!! meter —> 0.00 reward     

		Speed < 0.5 —> 50% discounted rewards      

		Turn more than 15 degrees —> 50% discounted rewards     

		return reward`     

<img width="1007" alt="Create model" src="https://user-images.githubusercontent.com/38410965/116016648-4789db00-a60b-11eb-941f-788ac55a06ed.png">

#

> In step three, you get to see the car, or the model, break pretty much all those rules early on.  So, that, it’s a lot of suffering down here, (trust me), but eventually it gets to where it’s sort of completing the track 100% of the time between epoch 240 up to 340 it looks like.     

### Step 3

**Training**     

<img width="492" alt="N" src="https://user-images.githubusercontent.com/38410965/116016663-52447000-a60b-11eb-898c-382ef33d3e16.png">

# 

> Step 4: you can evaluate your model, and it was able to make it around there, a different track, similar track, 100% over each one of the evaluations.  

### Step 4

**Evaluation**       

<img width="584" alt="Evaluation results" src="https://user-images.githubusercontent.com/38410965/116016677-5c666e80-a60b-11eb-960b-1ea0650f3452.png">

<img width="575" alt="Orthogonal" src="https://user-images.githubusercontent.com/38410965/116016687-67b99a00-a60b-11eb-9b1a-a78bd489b7f0.png">

#

> And in step five, you get to submit your model to a qualifier sometime this April, and the preliminary results were that I came in 242nd out of 379 submissions.  
So, thank you very much. Bye bye. 

### Step 5

**Let’s race**     

<img width="231" alt="242379" src="https://user-images.githubusercontent.com/38410965/116016711-8324a500-a60b-11eb-85ab-25b4a6c8fa1d.png">
