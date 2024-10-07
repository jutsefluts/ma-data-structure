Max Assist Data Structure Documentation

This document explains the structure of the data used in our lesson generator system.

1. Overall Structure

The data structure for the lesson generator is a single JSON object. This object has two top-level fields:

- lesson_prerequisites: An array of prerequisite questions for lesson generation
- lesson_structure: The main structure containing the generated lesson content

2. Lesson Prerequisites

The lesson_prerequisites is an array of question objects. Each question object has the following structure:

{
  "question_key": "",
  "question_text": "",
  "answer": ""
}

These questions typically cover:
- Target audience
- Lesson subject
- Intended learning outcomes

3. Lesson Structure

The lesson_structure contains four phases of a lesson:

- introduction: The introduction phase
- instruction: The instruction phase
- processing: The processing or practice phase
- conclusion: The conclusion phase

4. Content Objects

Each phase has a content array that can contain multiple objects of various types. These objects are used dynamically within a phase. The possible object types are:

a) Processed Text Object
b) Document File Object
c) Multiple Choice Question Object
d) Open Question Object

The number and combination of these objects within a phase can vary based on the specific needs of the lesson. For example, an instruction phase might contain several Processed Text objects followed by a Multiple Choice Question object, while a processing phase might primarily consist of Open Question objects.

Key points:
- A phase can contain any number of objects, including zero.
- Objects can be mixed and matched in any order within a phase.
- Not all object types need to be present in every phase or lesson.

This flexible structure allows for the creation of diverse and tailored lesson content.

5. UUID Field

The "uuid": "" field contains a unique identifier for each object, ensuring uniqueness within the lesson and across the application. The format can vary (e.g., standard UUID, shorter string, custom format) but should be consistent within the system.

6. YAML Conversion

JSON objects can be converted to YAML format. Refer to yaml_element_types_states.yaml for specific structures of:
- Processed Text (various states)
- Document File
- Multiple Choice Question (radios)
- Open Question (textarea)

7. AI Role in the Lesson Structure

AI contributes to various aspects of the lesson structure and content generation:

a) Prerequisite questions:
   - ai_feedback_prerequisites_prompt: Guide feedback on prerequisite answers

b) Introduction phase:
   - ai_introduction_prompt: Create effective introductions
   - ai_feedback_introduction_prompt: Evaluate and provide feedback on introductions

c) Instruction phase:
   - ai_instruction_prompt: Generate lesson instructions
   - ai_feedback_instruction_prompt: Assess and provide feedback on instructions

d) Processing phase:
   - ai_assignment_prompt: Create assignments based on initial questions
   - ai_feedback_assignment_prompt: Evaluate and provide feedback on assignments

e) Conclusion phase:
   - ai_conclusion_prompt: Generate appropriate conclusions
   - ai_feedback_conclusion_prompt: Assess and provide feedback on conclusions

f) Generate questions:
   - ai_question_prompt: Generate questions based on processed text

These prompts enable dynamic content generation and adaptation, with feedback mechanisms to improve lesson quality and effectiveness.