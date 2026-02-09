# Chapter 7 End-of-Chapter Assignments

### Assignment 4 

Compare Boehm’s hierarchy with McCall’s model in terms of granularity, stakeholder alignment, and metric operationalization.

###### Answer

Based on Section 7.1, the two models can be compared as follows::

1. Granularity

- Boehm: Exhibits higher granularity, specifically at the lowest level. The model provides "more detailed primitive constructs," offering a "deeper breakdown of quality attributes".
- McCall: Is less granular. The text explicitly states it is "less granular at the lowest level compared to Boehm's primitive constructs".

2. Stakeholder Alignment

- Boehm: Aligns with a comprehensive, holistic view that serves both users and system/hardware engineers. It covers a "broader range of characteristics," explicitly "integrating aspects of hardware performance" alongside user needs.
- McCall: Aligns strongly with the user's perspective. Its primary focus is on "precise measurement of high-level characteristics from a user's perspective" and places "strong emphasis on the user's view".

3. Metric Operationalization

- Boehm: Facilitates granular measurement. The detailed primitive constructs allow for a more specific analysis, which "facilitates more granular measurement and analysis" compared to McCall.
- McCall: Focuses on the measurement of high-level characteristics. It aims to measure abstract factors (like Reliability or Usability) directly from the user's viewpoint rather than building them up from granular primitive constructs.

# Chapter 8 End-of-Chapter Assignments

### Assignment 2 

Critically analyze why Security, Compatibility, and Safety became top-level characteristics in ISO/IEC 25010.

###### Answer

Security, Compatibility, and Safety became top-level characteristics in ISO/IEC 25010 because modern software systems became far more interconnected, mission-critical, and embedded in daily life. Security was elevated since treating it as a sub-feature of functionality no longer reflected the growing importance of protecting data and preventing cyber threats. Compatibility became its own category to address the need for systems to coexist and interoperate in cloud-based and distributed environments, rather than being implicitly handled through interoperability alone. Safety was added as a primary characteristic to explicitly recognize that software failures can endanger human life, property, or the environment. Overall, these changes reflect a shift from focusing mainly on internal software quality to addressing real-world risks and dependencies in today’s digital ecosystem.