# AWS DeepRacer  

TGIF project: What can I learn about AWS DR in one day?

Please click the video to hear sound or follow along with the slides and transcript below the video.

![demo](https://user-images.githubusercontent.com/38410965/111689560-92d9ee00-8802-11eb-9406-4075edc93d90.mp4)

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

	1.	<span style="color:red">some Evaluating completion text</span> > Training completion
		Stochastic reward 

		Exploitation vs. Exploration: 
		
			Evaluation is greedy.  Only looks for sure things.
			Training explores, revisits weaker action-state pairs.

	2.	Correlation ( Evaluating completion vs. (Reward & Training completion) ) < )

		Evaluating completion goes down
		Reward goes up & Training completion goes up

		Overfitting because of less exploration or less successful exploration. 
	 
		Evaluating completion goes up
		Reward goes down & Training completion goes down

		Generalizing because of more exploration or more successful exploration. 

#

> So, I found, you know, in doing this, (it was really easy), that the AWS DeepRacer is a great place to learn or apply reinforcement learning.  It has all the ingredients that you need: so, environment, state, agent, actions and rewards.  So, we’ve discussed the car already, and briefly touched upon the environment, but, you know, with more turns, obstacles, other racers, narrower roads, longer roads, you have more state accommodations to deal with, more complexities. So, you have to have a more complex model, which requires more time and money to run.  So, I ran my model about 2 hours, but if you had to do that over and over again, it could get kind of expensive. 

### 3. Great place to learn RL     

	✓	**RL ingredients**     
	environment —> states       —> agent —> actions                  —> rewards     
	race track     —> race type —> car      —> speed & steering —> points     

	✓	**Agent = car**     

	✓	**Environment = track** 
	turns      
	obstacles      
	other racers     
	narrower roads     
	longer roads (bigger batch size)     
	——> 	more state combinations      
	——> 	more complex agent needed     
			= more complex model     
			= more time & money     


#

> So, my objective for, you know this project was to play around with AWS a bit, to apply reinforcement learning concepts, to build a model, and to look under the hood of AWS and the model itself.   AWS makes easy to do this in just really, you know, 5 steps.  






### 4. Objective:     

	Play with AWS console      
	Apply RL Concepts      
	Build a time trial model     
	Under the hood     

**Novice with limited budget:**     
	environment = race track with gentle turns	     
	race type = time trial = alone on track     
	car = one headlight + no mirrors     
	actions = slow is 1m/s & steady has fewer steering clicks     
	rewards = not too slow, stay in middle, don’t turn too much     
	—> quickly training model     

**5 steps to submitting a model to the April time trials**     

**Later:**     
	better robot hardware     
		head to head     
		object avoidance     
		object recognition     
	better understanding      
		bootcamp videos (21 total)     
			https://www.aws.training/Details/eLearning?id=32143     
		AWS Training and Certification team:     
			https://www.aws.training/Details/eLearning?id=32143     

#

> Step zero is getting hooked up to AWS.  They make it real easy. I already had an account there.  The IAM roles were already set up, but it was interesting to see what the IAM roles are; they’re listed there.  The resources that are necessary: there are 5 sets of resources there, and they’re well documented.   So, that was also very interesting to see.  


### Step 0 = 5 minutes	     
		
**IAM roles defined in pop out if needed**	     
	⁃	AWS DR requires      
	⁃	Service Role —> resources & make calls     
	⁃	Maker Role —> SageMaker manage resources     
	⁃	RoboMaker Access Role —> RoboMaker manage resources     
	⁃	Lambda Access Role —> Lambda function calls resources     
	⁃	CloudFormation Access Role —> create/manage needed stacks     
	
**AWS Resources**      
	⁃	CloudFormation stack     
	Learn about AWS CloudFormation     
	⁃	S3 bucket     
	⁃	model configurations     
	⁃	training output     
	⁃	virtual circuit logs     
	⁃	Learn about AWS S3     
	⁃	AWS Lambda      
	⁃	test reward function —> training model     
	⁃	Learn about AWS Lambda     
	⁃	AWS RoboMaker / SageMaker     
	⁃	SageMaker training job     
	⁃	RoboMaker simulation     
	⁃	inside VPC (Virtual Private Cloud)     
	⁃	exchange data via S3     
	⁃	AWS RoboMaker simulation application     
	⁃	virtual AWS DR representation      
	⁃	onto     
	⁃	virtual representation of track     
	⁃	using rigid body physics simulator     
		—> predictions of real world behavior     

#

> Step one is, you know, learning reinforcement learning basics, and they walk you through this in several really concise slides.  


### Step 1 = Learn RL basics 

RL drives the DR     
Know RL —> create / optimize model that drives your car —> win     



#

> There’s the agent.  

### Step 1.1



#

> There’s the environment.  

### Step 1.2



**So easy: Will these become household words?**
	⁃	agent
	⁃	environment 
	⁃	action			
	⁃	state 			
	⁃	reward

#
 
> There’s the action. 

### Step 1.3

Action	= agents moves = steering angle + speed


#

> The states.  

### Step 1.4

state = camera feed + LIDAR + boxes on tarmac


#

> And the rewards. 

### Step 1.5 

Reward = environmental feedback to agent per action and state
		      defined by reward function 



#

> So, in step two, you create a model. So, we’ve already sort of gone through the car and the environment.  For rewards, I grafted together a couple different rewards snippets that they already had, and in the end, it ended up so that the car would not go too slow, it would not make too many turns, sharp turns, and would always remain in the center of the road.  

### Step 2 

**Create Model**     
	✓	Agent = car     
	✓	Environment = track     
	◦	Reward function:     

Give the dog a bone …     


**Grafted 2 different snippets:**     

Pseudocode:     

	`def reward_function:     

		Distance from center:          
			0.10 meter —> 1.00 reward     
			0.25 meter —> 0.50 reward     
			0.50 meter —> 0.10 reward     
	    	       #^$%@!! meter —> 0.00 reward     

		Speed < 0.5 —> 50% discounted rewards      

		Turn more than 15 degrees —> 50% discounted rewards     

		return reward`     



#

> In step three, you get to see the car, or the model, break pretty much all those rules early on.  So, that, it’s a lot of suffering down here, (trust me), but eventually it gets to where it’s sort of completing the track 100% of the time between epoch 240 up to 340 it looks like.     

### Step 3

**Training**     


# 

> Step 4: you can evaluate your model, and it was able to make it around there, a different track, similar track, 100% over each one of the evaluations.  

### Step 4

**Evaluation**       


#

> And in step five, you get to submit your model to a qualifier sometime this April, and the preliminary results were that I came in 242nd out of 379 submissions.  
So, thank you very much. Bye bye. 

### Step 5

**Let’s race**     
