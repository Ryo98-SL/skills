
# Ryo98's Skills

## There are several skills that help me to control AI's quality of generated code:

- ### package-guardrails
The purpose of this skill is to reduce the number of input tokens. 
Excessive context can lead to context anxiety and agents forgetting earlier information from the context[(context rot)](https://www.trychroma.com/research/context-rot). 
By focusing an agent on a single package and using it as a boundary, it prevents agents responsible for other packages from accidentally entering packages outside their management (restricting read/write access to packages not owned by them). 
This barrier also allows agents to collaborate without overwriting other agents' code, as they only modify their own packages.
If they want a dependent package to provide a feature or fix a bug, they will initiate an issue with the dependent module. 
When the agent responsible for the dependent package starts, it will first check its own issue and determine whether to resolve it.
If not, it will consult with a human and provide a reason.
Furthermore, this skill mandates that agents write two markup files for the package: README.md and README.deep.md. 
These files describe the current state of the package and help the agent in the next new dialog window obtain information, allowing it to better understand and modify the code. 
For details, please refer to the corresponding README.md file for the skill.
