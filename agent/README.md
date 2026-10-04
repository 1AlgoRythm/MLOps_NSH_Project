# Orchestrator and LLM steps

A fixed flow around the model calls: understand, plan, generate the query, choose charts, narrate. A larger model for planning and queries, a smaller one for cheap steps.

Python (LangGraph or a custom state machine); Claude through AWS Bedrock.
