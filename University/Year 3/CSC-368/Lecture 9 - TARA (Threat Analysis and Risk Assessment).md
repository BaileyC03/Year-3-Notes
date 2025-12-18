#### TARA Process Overview: 
- Asset identification
- Impact Rating
- Threat Enumeration
- Attack Path Analysis
- Attack Feasability Rating
- Risk Determination
- Risk Treatment Decision

#### 1. Asset Identification
- Identify the asset (something which has or contributes to value)
- Identify the security properties of that asset (STRIDE)
	- Confidentiality
	- Interity
	- Availability
 - Identify damage scenarios stemming from these properties not being present
 - Provide an impact rating for those damage scenarios

#### 2. Impact Rating: 
- 4 Categories: 
	- Safety
	- Finance
	- Operational
	- Privacy
- 4 Severities:
	- Severe
		- (Safety) Life threatening Injuries [Survival Uncertain]
		- (Finance) Catastrophic financial consequences
		- (Operational) Core function damaged
		- (Privacy) Massive misuse of personal data
	- Major
		- (Safety) Severe and life-threatening injuries [Survival Probable]
		- (Finance) Substantial financial consequences
		- (Operational) Important function damaged
		- (Privacy) Privacy damage has serious impact
	- Moderate
		- (Safety) Light and moderate injuries
		- (Finance) Inconvenient financial damage
		- (Operational) Partial degradation of vehicle function
		- (Privacy) Privacy consequences are inconvenient
	- Negligible
		- (Safety) No injuries
		- (Finance) Financial damage has no effect, is negligible or irrelevant
		- (Operational) No impairment or non perceivable impairment of function
		- (Privacy) Privacy damage has no effect, is negligible or irrelevant

#### 3. Threat Enumeration
- The identification of potential threats that can compromise the security or integrity of a system

#### 4. Attack path analysis: 
- The threat scenarios should be identified and analysed to aid in describing possible attack paths. 
- There are variying methods to do it: 
	- Top down: Identifying high level threats and drilling down into specific details and vulnerabilities.
- Attack path example: 
	-  Gaining physical access to an onboard system
	- Cloning the signal emitted by a given keyfob.

#### 5. Attack feasability rating
- You get 5 categories:
	- Elapsed Time
	- Expertise
	- Equipment
	- Knowledge required of the item
	- Window of oppurtunity
- and assign them points accordingly. From this, you sum their points to get a total attack feasability score. 

#### 5.1 Elapsed Time:
- <1 week, 0 points
- <1 month, 1 point
- <= 6 months, 4 points
- 3 years, 10 points
- >3 years, 19 points

#### 5.2 Expertise Required
- Layman (Unknowledgable, think googled steps), 0 points.
- Proficient (Baseline knowledge, experienced owner / technician), 3 points
- Expert (Understands hardware, algorithms etc...), 6 points
- Multiple experts (different fields of expertise), 8 points

#### 5.3 Equipment Required
- Standard (Can be bought on amazon), 0 points
- Specialised (Can be acquired with medium effort), 4 points
- Bespoke (Black market tools, very specialised or restricted), 7 points.
- Multiple bespoke, 9

#### 5.4 Knowledge of the item required
- Public (Can be googled), 0 points
- Restricted (Within dev orgs and under an NDA), 3 points
- Confidential (Knowledge shared between discrete teams within dev org, need to know basis), 7 points
- Strictly confidential (Known only by a few individuals), 11 points

#### 5.5 Window of oppurtunity
- Unlimited (High availability via public network without time limitation) 0 points
- Easy (High availability but limited access time. Remote access etc.) 1 point
- Moderate (Low availability / low phisical or logical access. Special tools not needed) 4 points
- Difficult (Very low availability of item or component, impractical level of access to the item or component) 10 points.

#### 5.6 Totalling:
Total score:
- 0-9 - High attack feasibility
- 10-13 - High attack feasibility
- 14-19 - Medium attack feasibility
- 20-24 - Low attack feasibility
- 25+ - Very low attack feasability

#### 6. Risk Determination:
![[Pasted image 20251217140833.png]]

#### 7. Risk Treatment Decision:
You have a few options here: 
- Avoid the risk somehow
- Reduce the risk 
	- Deriving security goals and requirements
- Sharing or transferring the risk 
	- Third parties may be able to keep you more secure, like cloudflare or ISP providers,
- Accepting the risk
	- Firming the L
