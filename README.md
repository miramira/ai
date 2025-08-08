# Multi-Agent Systems

Instead of writing long, complex prompts that may not deliver results reliably, you can construct a flow of multiple, simple agents that can collaborate on complex problems by dividing tasks and responsibilities.

This architectural approach offers several key advantages such as:

* Easier to design: You can think in terms of agents with specific jobs and skills.
* Specialized functions with more reliable performance: Specialized agents can learn from clear examples to become more reliable at their specific tasks.
* Organization: Dividing the workflow into distinct agents allows for a more organized, and therefor easier to think about, approach.
* Improvability and maintainability: It is easier to improve or fix a specialized component rather than make changes to a complex agent that may fix one behavior but might impact others.
* Modularity: Distinct agents from one workflow can be easily copied and included in other similar workflows.

# The Hierarchical Agent Tree
![](/images/agent_tree.png "This is a sample image.")

 This helps limit the options for transfers for each agent in the tree, making it easier to control and predict the possible routes the conversation can take through the tree. Benefits of the hierarchical structure include:

* It draws **inspiration from real-world collaborative teams**, making it easier to design and reason about the behavior of the multi-agent system.
* It is **intuitive for developers**, as it mirrors common software development patterns.
* It provides **greater control over the flow** of information and task delegation within the system, making it easier to understand possible pathways and debug the system. For example, if a system has two report-generation agents at different parts of its flow with similar descriptions, the tree structure makes it easier to ensure that the correct one is invoked.

The structure always begins with the agent defined in the **root_agent** variable (although it may have a different user-facing **name** to identify itself). The root_agent may act as a **parent** to one or more **sub-agents**. Each sub-agent agent may have its own sub-agents.
