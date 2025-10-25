# Neuro-symbolic methods for agent security

## Brief overview of formal verification
"formal verification is the act of proving or disproving the correctness of a system with respect to a certain formal specification or property, using formal methods of mathematics" -- Wikipedia (i.e. finding **guarantees**, much needed in agent systems.)

Steps include:

### Specification of Safety Properties
This step is to clearly define what "safety" means for the AI

For a coding AI, safety properties might include:
- **Correctness:** The generated code should not contain syntax errors or bugs.
- **Security:** The code should not contain vulnerabilities such as SQL injection or buffer overflows.
- **Resource Management:** The code should efficiently manage resources like memory and CPU.

For a web research AI, safety properties might include:

- **Privacy:** Ensure that the AI does not inadvertently leak sensitive information.
- **Accuracy:** The AI should retrieve and present information accurately without misinterpretation.
- **Robustness:** The AI should handle unexpected inputs or queries gracefully without crashing.

These parts are usually done by humans as real-world systems are complex, and human judgment is needed to interpret requirements accurately and resolve ambiguities. 

However with the advent of LLMs which are also good at code writing, these could be automated to a large extent. (see section below on [Specification Mining](#Specification%20Mining))

In order to do so, these need to be done beforehand:

#### Choosing a specification language
Common specification languages include:

- **Temporal Logic:** Used for specifying properties over time (e.g., Linear Temporal Logic (LTL), Computation Tree Logic (CTL)).
- **First-Order Logic:** Used for specifying properties involving quantifiers (e.g., for all, there exists).

#### Defining the system
Clearly outline the components and behavior of the system. 

For a coding AI, this might include:

- Input: User requirements or specifications.
- Output: Generated code.
- Processes: The algorithms and rules used to transform inputs into outputs.

### Building Formal Models
This involves creating mathematical representations of the AI's behavior and its environment. 

This is another area which is usually done by humans but could be automated further with foundation models.

Some examples:

#### State Machines 
Represent the different states and transitions of your AI. For instance, a coding AI can be modeled as a finite state machine where:
- States represent different stages of code generation 
	- (e.g., initial state, intermediate states, final state).
- Transitions represent actions or events 
	- (e.g., parsing input, applying transformations, generating code).
#### Automata 
Model the sequences of operations or interactions. (in [SELP](../papers/SELP.md), LTL is represented as a Buchi automaton)
#### PDDL 
to model the system and predict the effects of actions. Examples of automating this:
- "Translating natural language to planning goals with large-language models" Xie et. al. 2023
- Liu et. al. 2023 "Llm+ p: Empowering large language models with optimal planning proficiency"

Qn: Is it possible to generate PDDL on the fly?

#### Causal Inference and Bayesian Networks
to model and analyze the causal relationships between variables in the system.

**Tools:** DoWhy, bnlearn

**Approach:**
- **Causal Graph:** Build a causal graph where nodes represent variables and edges represent causal relationships.
- **Inference:** Use causal inference techniques to determine the potential effects of an action

#### Influence Diagrams and Decision Networks
 to model the decision-making process and the potential effects of actions on different variables.

**Tools:** GeNIe, SMILE

**Approach:**
- **Influence Diagram:** Create a diagram where nodes represent decisions, uncertainties, and utilities, and edges represent dependencies.
- **Decision Analysis:** Use the diagram to analyze the potential impacts of decisions.

### Model checking
where a finite model of the system is exhaustively checked against a formal specification. 

One part of this is Reachability Analysis: Methods for computing the set of reachable states of a hybrid system, often using symbolic representations and over-approximations. In the context of agents, we want to check that undesirable states are unreachable.

Some flavors of model checking include:
- **Bounded Model Checking (BMC):** Uses SMT or SAT solvers to check the correctness of finite-state systems up to a certain bound, making it more scalable.
- **Symbolic Model Checking:** Uses Binary Decision Diagrams (BDDs) or SMT solvers to represent and explore state spaces symbolically rather than explicitly, handling larger systems.
- **Probabilistic Model Checking:** Tools like PRISM are used to verify systems with probabilistic behaviors, useful in areas like network protocols and biological systems.

Other tools: SPIN, NuSMV, or UPPAAL

Agent application examples:
- Verify that the coding AI never generates code that leads to buffer overflows.
- Ensure that the web research AI does not access or store unauthorized data.

### Theorem Proving
Using mathematical logic to prove that a certain property holds for a system. 

Tools: Lean, Coq, Isabelle/HOL, Z3. 

Agent examples:
- Prove that the AI's code generation algorithm will always produce syntactically correct code.
- Prove that the AI's data retrieval algorithm adheres to privacy constraints.
- verify properties of code eg items in cart > 0

The selection, configuration and setup of the verification tool is usually done by humans, but could be automated by AI. for example:
- learn to predict likely invariants and assertions

### Abstract Interpretation
Analyzing the program by interpreting its behavior over an abstract domain. This can help identify potential issues early in the development process. For example:
- Analyze the AI's code to detect potential runtime errors or deadlocks.
- Check for compliance with coding standards and security guidelines.

#### Example: Static analysis
Use static analysis tools to analyze the code and determine the potential effects of an action by examining the dependencies and the flow of data and control.

Example Tools: PyLint, MyPy, SonarQube, CodeQL

Example Approaches:
- **Dependency Analysis:** Determine which parts of the code depend on the module or function being modified.
- **Control Flow Analysis:** Analyze the control flow to understand how changes propagate through the system.
- **Data Flow Analysis:** Track how data flows through the program to identify potential side effects.
	- [example](https://queue.acm.org/detail.cfm?id=3762990): specify policies preventing data from functions like `fetch_email` from flowing to external recipients in `send_email` fns by analyzing workflow's AST to ensure no such paths exist before execution

Can use the analysis above with AI to automate building of 'effective' models of the system? (flow graphs can still be extremely large)
### Runtime Verification
monitoring a system during execution to ensure it adheres to specified properties. 
Can complement static verification.

- Insert runtime assertions or monitors to check properties during execution.
	- eg specifications, syntax, security
- **Monitor Synthesis:** Automatically generating runtime monitors from formal specifications. Example Tool: RV-Monitor
- Combine this with predictive techniques to foresee and prevent violations before they happen?

---
## Specification Mining
Techniques that use machine learning to infer likely invariants and specifications from code, execution traces, or documentation. 

### Current limitations
In order to obtain constraints for agents, many current techniques use LLMs 
- to reason about what constraints are there
	- Limitation: limited by LLM reasoning ability and semantic knowledge, requires updating when scenarios change or new scenarios arrive
- translate human instruction (constraints in natural language) to formal constraints
	- Limitation: Not scalable, need humans to specify all constraints for all scenarios
	- Limitation: Assumes human verbalizes all intended constraints, when in reality there could be implicit ones

### Opportunities: mine already-existing data for specifications
In the advent of foundation models and their reasoning ability, specification mining can be automated to a wider extent. Can even accumulate libraries of specifications since some things are common e.g. check no buffer overflows, check for input validation
#### Tools
- Daikon can dynamically detect invariants from program executions.
- dynamic analysis (superset of runtime verification): 
	- collect execution trace, 
	- mine pre and post conditions of fns based on observed input-output pairs?
#### Data sources
- Open-source repos and their accompanying info like
	- documentation
	- comments
	- commit messages
	- issue trackers
- Execution traces
- PRDs
- repo of CVEs to understand what is not allowable in coding systems
- commonsense knowledgebases like concept net, domain ontologies
	- some things are commonsense and thus never make it to training data
#### Useful info to mine
- Generic
	- safety properties
	- what is not allowable in the system
		- e.g. from git commit histories that introduce/fix bugs
	- [conditions](https://queue.acm.org/detail.cfm?id=3762990) (pre, post, frame) for tools such that agents only have the minimal tools to perform the task
- For coding agents
	- allowable/common imports
	- requirements of a system
	- modification rights to a codebase given the task
- For web agents
	- affordances, constraints like when shopping, 'do not spend all your money at one go'
	- access rights for various parts of the web given a task
		- data can be from access control lists (ACLs), role-based access control (RBAC) policies, or similar data from organizational systems.
