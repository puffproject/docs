
# Endpoints
This document is for outlining ideas about the api structure for unity-test. Swagger documentation to follow, hopefully with OpenAPI 3.0.

# Course-Management Endpoints
Course management microservice endpoints

## Course
**POST** `/course`: Create or update a course

body={Course}

**GET** `/course`: Get courses

?id={course id}
?code={course code}
?level={course level}
?term={course term}
?academicYear={course academic year}

**DELETE** `/course/{courseId}`: Delete a course

**POST** `/course/{courseId}/attr`: Create or update a course attribute

body={CourseAttribute}

**GET** `course/{courseId}/attr`: Get attributes for a course

**DELETE** `course/{courseId}/attr/{courseAttributeName}`: Delete a course attribute

## Assignments
**POST** `/assignment`: Create an assignment

body={Assignment}

**GET** `/assignment`: Get assignments

?id={assignment_id}
?name={assignment_name}
?course.code={course_code}
?course.term={course_term}
?course.level={course level}
?course.academicYear={course academic year}

**DELETE** `/assignment/{assignmentId}`: Delete an assignment

**POST** `/assignment/{assignmentId}/attr`: Create an assignment attribute

body={AssignmentAttribute}

**GET** `/assignment/{assignmentId}/attr`: Get attributes for an assignment

**DELETE** `/assignment/{assignmentId}attr/{assignmentAttributeName}`: Delete an assignment attribute

## Engagement

### Vote
**POST** `/engagement/{sourceName}/{itemId}/vote`: Vote on a source item

?action={upvote | downvote | novote}

### Comment
**POST** `/engagement/{sourceName}/{itemId}/comment`: Comment on a source item

body={Comment}

**GET** `/engagement/{sourceName}/{itemId}/comment`: Get comments on a source item

?id={commentId}
?author={authorUsername}

**PUT** `/engagement/{sourceName}/{itemId}/comment`: Update a comment on a source item

body={Comment}

**DELETE** `/engagement/{sourceName}/{itemId}/comment/{commentId}`: Delete a comment on a source item (Restricted to owner of comment or admin)

### Stats
**GET** `/engagement/{sourceName}/stats`: Get the statistics of (a) source item(s)

?ids={itemIds}[]

## User
**GET** `/user/assignments`: Get the user's assignments (References user enrollments)

?assignment.id={assignmentId}
?assignment.name={assignmentName}
?assignment.course.code={courseCode}
?assignment.course.term={courseTerm}
?assignment.course.academicYear={classAcademicYear}
?pinned={true | false}

Should be able to sort to get the pinned assignments at the top of the results.

**POST** `/user/assignment/{assignmentId}/enroll`: Enrolls the user in an assignment

?pin={true | false} (Set the pinned status of the assignment for the user)

**DELETE** `/user/assignment/{assignmentId}/unenroll`: Removes a user's enrollment in an assignment

**GET** `/user/engagement/{sourceType}/{sourceItemId}/vote`: Get the user's vote on a source item (Check if a user has already voted on something) (may not be necessary, to be seen) 

# Test Runner Endpoints

Test runner microservice endpoints

## Submissions
Handle file submissions

**GET** `/download`: Download source code upload. Allows a user to download a copy of their uploaded source code. (Secured for author or admin)

?submissionId={submissionId}

**POST** `/upload`: Upload source code files. Allow user to upload source code to run test cases against.
(In form data)

?assignmentId={assignmentId}
?files={file}[]

## Test Suite
**POST** `/suite`: Create a test suite for an assignment

body={Suite}

**GET** `/suite`: Get test suites

?id={suiteId}
?assignmentId={assignmentId}
?name={suiteName}
?lang={programming language}

**DELETE** `/suite/{suiteId}`: Delete a test suite (Restricted to creator or admin)

**POST** `/suite/{suiteId}/run`: Run test cases in test suite

?ids={test case ids to run in the suite}
?limit={number of cases to run if ids not specified}
?submissionId={id of source code submission to use, otherwise use latest}

**POST** `/suite/{suiteId}/setFile`: Upload test file for a test suite

**GET** `/suite/{suiteId}/getFile`: Get the contents of a test file for a test suite

**POST** `/suite/{suiteId}/vote`: Vote on a test suite. (System-level restricted)

?action={upvote | downvote | novote}

## Test Case
**POST** `/case`: Create a test case for a test suite

body={Case}

**GET** `/case`: Retrieve a pageable view of test cases

?id={caseId}
?name={functionName}
?suiteId={test suite id}
?lang={Programming language}

**PATCH** `/case`: Update a test case. (Restricted to author or ADMIN)

body={Updateable fields in Case}

Updateable fields
* code
* description

**DELETE** `/case/{caseId}`: Delete a test case (if you are the author or ADMIN)

**POST** `/case/{caseId}/vote`: Vote on a test case. (System-level restricted)

?action={upvote | downvote | novote}

## User
**GET** `/user/cases`: Get test cases written by the user

**GET** `/user/recentUploads`: Get source code submissions uploaded by the user

**GET** `/user/suites`: Get test suites created by the user
