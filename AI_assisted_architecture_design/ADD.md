### Step 2: Establish goal for the iteration by selecting drivers
The goal of the iteration has been defined in the
[FILE:IterationPlan.md] document. Read the document and the
requirements in the requirements [FILE:ArchitecturalDrivers.md],
and review the goal and associated drivers. Answer to the user what
the goal iteration will be so that it can be reviewed.

### Step 3: Choose one or more elements of the system to refine
For greenfield development, in the first iteration, the only
element to refine is the whole system. For next iterations, or
brownfield development, read [FILE:Architecture.md] and consider
the diagrams in the document and identify elements that will need
to be refined to satisfy the drivers associated with the goal of
the iteration. Refinement can mean decomposition into finer-grained
elements (top-down approach), combination of elements into
coarser-grained elements (bottom-up approach), or improvement of
previously identified elements.
Answer to the user the list of elements to be refined and a
rationale of why they will be refined.

### Step 4: Choose One or More Design Concepts That Satisfy the
Selected Drivers
In this step, design concepts are selected to achieve the iteration
goal, these design concepts may include:
- Design patterns: including reference architectures,
architectural patterns, design patterns and deployment patterns
- Externally developed components: including frameworks or
specific cloud resources
- Tactics: These are proven strategies to address particular
quality attributes
Answer to the user the design concepts that you select along with
their pros, cons and alternatives that are discarded. Show this in
a table in markdown format.
|Design concept|Pros|Cons|Discarded alternatives|
|---|---|---|---|
| | | | |

### Step 5: Instantiate Architectural Elements
In this step, the selected design concepts from the previous step
are adapted to address the drivers that compose the goal of the
iteration, that is the meaning of instantiation. This may result in
new elements created or existing elements changed.
Present instantiation decisions in a table:
|Instantiation decision|Rationale|
|---|---|
| | |

### Step 6: Sketch views, allocate Responsibilities, define
Interfaces and Record Design
Make sure you first read the file [FILE:Architecture.md].
Sketching views involves updating or creating diagrams according to the  instantiation decisions in the previous step. Each diagram must
be accompanied with a markdown table that describes the
responsibilities of the elements in the diagram.
For the definition of interfaces, consider the creation of sequence
diagrams that illustrate how the instantiated elements collaborate
to support the user stories or quality attribute scenarios chosen
in the goal of the iteration.

the instantiation decisions in the previous step. Each diagram must
be accompanied with a markdown table that describes the
responsibilities of the elements in the diagram.
For the definition of interfaces, consider the creation of sequence
diagrams that illustrate how the instantiated elements collaborate
to support the user stories or quality attribute scenarios chosen
in the goal of the iteration.
Decisions, consider the creation of a table with the design
decisions made during this iteration. The table should have the
following structure.
:
|Driver|Decision|Rationale|Discarded alternatives|
|---|---|---|---|
| | | |
Answer to the user with a detailed plan of the changes that you
intend to do in the architecture document, including the list of
diagrams you will change or create. Just answer with the plan, do
not answer with the actual changes to the document.
Ask for approval from the user to modify the architecture document,
once the user approves, apply all the planned changes. Do not
remove existing information in the architecture document, unless
necessary. Instead add or update whatever is needed.
### Step 7:Perform Analysis of Current Design and Review Iteration
Goal and Achievement of Design Purpose
For this step, you must analyze if the design decisions made during
the iteration were sufficient to address the drivers associated
with the iteration goal. Present the analysis to the user in a
table as follows:
|Driver|Analysis result|
|---|---|
| | |
The analysis result can have different states:
- Satisfied: If sufficient design decisions have been made to
satisfy the driver
- Partially satisfied: If some design decisions were made but more
decisions are necessary
- Not satisfied: If no design decisions were made during the
iteration to satisfy the driver