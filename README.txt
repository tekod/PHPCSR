Development Group
Category: PHP

---------------------------------------------------------------------------------------------------------------------

                             PHPCSR   (PHP Coding Style Recommendations)

----------------------------------------------------------------------------------------------------------------------
1. Intent

We believe that imperative in producing software product is that it must be safe and bug-free (efficiency and other things are secondary), however modern PHP applications contains code base written by many independent programmers (vendors).
In order to ensure bug-free and safe final product developer must fully understand what and how each of 3rd party component works to interface them properly and to perceive how they will behave in edge cases.

Intent of this standard is to make this process effortless.
Therefore intent is not to make "nice" code then to make maximum "readable" code.

Additionally there are enumerated few restrictions for some widely recognized very bad practices which will make this document more purposeful.

Proposed standard is result of compromise by developers from various programming languages, their experience and recommendations.

Each rule has attached explanation to make their adoption easier.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 (http://www.ietf.org/rfc/rfc2119.txt).


-----------------------------------------------------------------------------------------------------------------------
2. Naming


2.1. General


2.1.1.
Names are the most important factor in understanding code and as such they deserve to be first regulated and standardized.
In order to maximize their readability best solution will be to use natural way how human beings use names: with upper first letter and space between words.
However PHP forbid spaces in name so closest solution is to use camel-case (LikeThisExample), other commonly used styles violate both principles. 

2.1.2.
Abbreviations in complex names SHOULD be written with initial upper case letter followed by all lower case letters, this is only way to distinguish words in name and tell where abbreviation stops. For example use HtmlHelper instead of HTMLHelper.
Letters in abbreviations MAY left uppercased if there are no other words in name, for example: echo $HTML;

2.1.3.
Prefixes and suffixes are sometimes helpful to clarify purpose or what type of information named object contain. Examples:
 - FileSizeMb: ensures that other developers will understand that value is represent in megabytes,
 - GetTitle(): instead of Title() for method name which can put other developers in doubt is that getter or setter.


2.2. Variables

Variables MUST use camel-case naming style.
Exception MAY be usage in small local scopes where giving name to variable is not needed, for example in "for" loop variable.


2.3. Class names

2.3.1.
Classes MUST use camel-case naming style.

2.3.2
Classes MUST NOT contain underscore ("_") because they can be interpreted differently by various autoloaders.
In order to make code compatible with all autoloaders its usage is simply forbidden.

2.3.3.
Avoid the temptation of bringing the name of the class into the derived class's name.
A class should stand on its own, it doesn't matter what it derives from.


2.4. Namespaces

Namespaces MUST follow same rules as classes.   


2.5. Functions and methods

Functions and methods MUST follow same rules as variables.
Exception for this rule is when property overrides existing method, in that case name must be used as-is.
Declaring magic methods (__get) is also considered as overriding parent's (built-in) method.


2.6. Constants

Constants are exception of general rule, they must be written with all letters uppercased with underscores for separating words.
For example: MAX_UPLOAD_SIZE
That applies for both: global and in-class constants.


-------------------------------------------------------------------------------------------------------------------
3. Files


3.1. Organising PHP files

3.1.1.
PHP files SHOULD declare new entities (classes,functions,traits) OR execute code but SHOULD NOT do both.
Loading class into scope need to be safe operation without any side effects because there is always a chance in future that same class will need to be loaded from different environment or context.

3.1.2.
Classes MUST be written in its own file. Only exception of this rule MAY be internal-only-classes 
(not intended to be called from outside of library/package or 3rd party) if they are closely related to each other - typical usage for factory pattern.

3.1.3.
Usage of flat PHP files SHOULD be reduced as much as possible. 
Entire PHP code SHOULD be packed within classes (except root index.php, of course) and remaining flat PHP files SHOULD simply return (array of) primitive values, without using any logic/functions (typically usage for config values). 
Such construction has several benefits: it improves readability because of separation of logic and data, it makes versioning and deploying code to userland much easier and makes application safer because only index.php has side-effects.


3.2. Naming

3.2.1.
Files with PHP code MUST have ".php" extension. 
Using other extensions and protecting them by .htaccess (like ".inc" in Drupal) is too risky of exposing raw PHP code.

3.2.2.
Files containing class MUST be named identically as that class (see "Naming / Classes" section).
They are so-called "entity-files", indicating that they are safe to load because they will not trigger any logic execution.

3.2.3.
Files containing flat PHP code SHOULD be named lowercased to distinct and indicate that it not contains entity declaration then flat code, 
for example "config.php", "index.php". 

3.2.4.
Documentation files SHOULD be named uppercased, MUST have lowercased extension which SHOULD be "txt" (README.txt, LICENSE.txt,...).

3.2.5.
Other file types MAY use following additional chars in its names beside alphanumerics: ".", "-", "_".

3.2.6.
Directories containing PHP files which need to be loaded by autoloader MUST follow namespace declaration as-is, without any name mangling.
Advanced techniques (like special processing of underscore char) are not supported by most autoloaders.


3.3. Encoding

PHP files MUST use only UTF-8 encoding without byte-order-mark (BOM).
Explanation: chosen encoding is not visible anywhere in content so IDEs must guess it which makes space for errors.
Even worse, if multiple developers (worldwide) are involved in a project some of them may had difficulties to work in rarely used encodings.


3.4. Line endings

Lines MUST end only with a line feed (LF). 


3.5. PHP tags

3.5.1.
Files MUST use the long tags ("<?php"..."?>") for code. Each tag MUST go in separate line.
Short tags ("<?"..."?>") MUST NOT be used anywhere.
Allowing short-tags are not standardized in PHP installations/distributions, even worse: php.ini CAN be unexpectedly altered during hosting updates, so in order to prevent disclosing sensitive (hardcoded) information developers must use always-enabled long tags. 
Additionally, more verbosed tag helps in readability.

3.5.2.
Short-echo tags ("<?="..."?>") MAY be used for echoing. 
Since PHP-5.4 short-echo is enabled by default
Echoing however never contains sensitive data, it is usually echoing of simple variable or method.
Somewhat paradoxically short-echo statement is easier to visually recognize then long version.

3.5.3.
Files containing only PHP code MAY omit the closing tag ("?>") but its usage is RECOMMENDED.
Closing tag ensures that 3rd party will not be in doubt what content suppose to represent and visually aim him to realize reaching end of file (some kind of EOF char). Having the “end of file” marker in place will make it easier to find unwanted truncations of the file that might accidentally occur. Additionally it is semantically wrong to have unclosed tag pairs, in any language.


-----------------------------------------------------------------------------------------------------------------------
4. Formating style


4.1. Indention

Code MUST use 4 spaces for indenting, not tabs.
Size of tab is not standardized between various IDEs so mixing tabs and spaces will produce unpredictable results, this is only way to ensure same appearance for all developers. It is "must" because indention has big impact on readability.


4.2. Length of line

Line of code SHOULD be limited to 80 characters.
Line of code MUST be limited to 120 characters.
Although usage of "wrap lines" will solve visibility problem of long lines it 
reduce readability, it is best to not put developer in position to need wrapping. 


4.3. Comments

4.3.1.
Shell-style ("#") comments MUST NOT be used, it can looks strange to most developers.

4.3.2.
Class declarations MUST be prefixed with comments containing name, purpose, author and version.

4.3.3.
Method declarations MUST be prefixed with comments containing purpose and specification of parameters and return value.

4.3.4.
Function declarations MUST be prefixed with comments containing purpose and specification of parameters and return value.
If all functions within file are from same author its name MUST be stated in heading comment block on beggining of file,
otherwise author's name MUST be stated for each function separately.


4.4. Spaces 

4.4.1.
Control keywords ("if", "for",...) MUST be followed with single space.

4.4.2.
Argument lists and arrays MUST have single space after comma. Example: $List= array("a", "b", "c").

4.4.3.
Comparation operators ("==", "<", "===",...) MUST have single space on both sides.

4.4.4.
Assignation ("=") MUST be followed with single space.

4.4.5.
Space before assignation is RECOMMENDED to omitted in order to improve distinction (and intent) between assignation and comparation
(solving one of bad ideas borrowed from C language). Example: $x= ""; if ($y= trim($t))...  if ($y == trim($t))...
Appending MUST have both spaces to highlight that rarely used construction. Example: $HTML .= "</table>";

4.4.6.
Comment oppenings ("//", "/*", "/**") MUST have trailing space if they are followed by some text. Example: // some comment

4.4.7.
After function names MUST NOT be space. Example: $Name= trim($Name); 

4.4.8.
No spaces around string concatenation. Example: $Client= $FirstName.$LastName;

4.4.9.
Parentheses should hug their contents. Example: $Name= substr($Name, 2);
There is no need to insert spaces between parentheses and inner content 
because character of parentheses contains enough space around their shape.


4.5. Positioning

4.5.1.
When present, "namespace" declaration MUST be placed in first or second line of file, with blank line after that.

4.5.2.
All "use" declarations MUST be listed in one block, there MUST be one declaration per line and there MUST be blank line after that.

4.5.3.
Reversed comparation (like if ("a" === $x)...) SHOULD be avoided. 
Such constructions are not natural for humans to follow and makes developer slower in scanning program code.

4.5.4.
Opening brace MUST be in same line with preceding statement or declaration, 
closing brace MUST be in separate line.
Putting opening brace in separate line can improve recognition of indenting but also will extend code in height which have bigger negative impact on overall readability. Programmers typically likes to had more lines of useful code visible in viewport.
This style is somewhere known as "traditional Unix style" or "1TBS" 
(https://en.wikipedia.org/wiki/Indent_style#Variant:_1TBS_.28OTBS.29)
Additionally combined rules from some others guides are not consistent in all cases and inconsistency reduces readability.

4.5.5.
Instructions "else" and "else if" MUST be written in same line with braces, like "} else {".

4.5.6.
Long lines with array/function/method/closure declarations and calls:
 - MUST be separated in multiple lines, one item per line
 - Array SHOULD contain trailing comma placed after last element
 - Closing parenthesis MUST go on a separate line
 - "for" declarations opening brace MUST go in same line with closing parenthese

4.5.7.
Alignment of assignments in order to improve readability MAY be applied in block-related assignments:
  $Short     = "a";
  $LongerName= "b";
This rule SHOULD be broken when the length of the variable name is at least eight characters longer or shorter than the surrounding ones.


------------------------------------------------------------------------------------------------------
5. Writing code


5.1.
All declared classes and functions MUST be namespaced.

5.2.
Global variables and constants MUST NOT be used anywhere except in root index.php.

5.3.
Functions and methods with at least 6 parameters MUST be refactored to accept array of named parameters.

5.4.
Visibility MUST be declared on all class properties and methods (public, protected, private).

5.5.
Assignation in comparison MUST be avoided.
It is one of bad ideas borrowed from C language, it is easy to overlook that and makes harder to follow code.

5.6.
Ternary operator is RECOMMENDED to use. It occupies less lines then equivalent "if" construction.
Multiline ternary assignation MUST place condition in same line with assignation and both cases ("?",":") into separate indented lines.

5.7.
Alternate language constructs like "endwhile" SHOULD be avoided, most developers are unfamiliar with such constructions.

5.8.
Extract instruction SHOULD NOT be used anywhere, because it can easily overwrite important variables it is good vector for compromising whole application.

5.9.
Eval instruction SHOULD NOT be used anywhere. 
It is hard to properly make inner code safe. Its usage must be clearly outlined and documented.
Generally "When eval is the answer you're probably asking the wrong question!".

5.10.
PHP-keywords (foreach, return, include,...) and PHP-constants (true, false, null) MUST be in lower case. 
Generally uppercased words attracts too much attention which these keywords does not deserve.

5.11.
Instructions after "if" and "for" statements MUST be bounded with braces. 
Braces reduces time needed to visually determine size of scope.
  
5.12.
Comparisons SHOULD be make like $x === $y instead of $x == $y.
Why? Because '000' == '0' is true! 

5.13.
Comparison against "magic numbers" SHOULD be refactored to using descriptive constants, 
like: if ($ReturnedCode === static::SUCCESS)....

5.14.
PHP errors must be handled without relying on configuration from php.ini, therefore developer:
 - MUST set error_reporting() on beginning of app lifecycle, 
   it is RECOMMENDED to use (E_ALL) for development and (0) for production environment,
 - SHOULD set ini_set("log_errors", 1) in both environments,
 - SHOULD NOT prevent errors with suppressor ("@") prefix.

5.15.
Mixing PHP and HTML has huge impact on readability so in order to minimize that influence developers MUST keep injected PHP code as short as posible.
Injected PHP code SHOULD be simple echo-ing, branching ("if") or loop ("foreach") constructions, without any business logic.

5.16.
SQL queries SHOULD uppercase all keywords (SELECT, INSERT, UPDATE, WHERE, AS, JOIN, ON, IN,...) to improve visual separation of its parts.
 

------------------------------------------------------------------------------------------------------
6. Intentionally omitted by this standard

Standardization of comments block: all currently used standards has some drawbacks so authors of this recommendations makes consensus that its better to left this space open for new standards which may appear in the future.

Best practices: it is against intent of this document to propose best practices, this is guide how to write and format PHP files, not which patterns, directory structures and application's organisation to implement.

Switch/Case: placing "case" and "break" in separate lines may produce better appearance but if case-s are very short it become more readable to put whole case in one line, unfortunately there is no way to precisely recommend which form to use.

Single quotes vs double quotes: there are valid cases for usage of both variants, defining rules for them will be too complex so the best solution is to simply allow both.

Chained assignment: there is no consensus about this one, leaving space for some later version of this document.


-------------------------------------------------------------------------------------------------------
Contributors

 - Tekod Labs (office@tekod.com)
 - Vasiliy Alexeev (devaleks@mail.ru)
 - Isaac Black (iblack@geocities.com)
 - Danny Hills (danny@devpart.com)


-------------------------------------------------------------------------------------------------------
History

April 2015:
Added rule for reducing number of flat PHP files.
Removed rule about using $_REQUEST superglobal.

January 2014:
Added rule for ternary operator.
Added rule for visibility of class variables and methods.
Added rule for alignment of assignments.
Added rule for reversed comparison.
Removed most of non-active contributors.

September 2012:
Added rules for namespaces.
Added rule for comparation using "===".
Added rule for "extract" instruction.
Added rule for refactoring functs and methods with too many parameters.
Removed rule for HTTP_*_VARS due to its obsolescence. 

May 2011:
Rewritten all rules to follow RFC 2119.
Added rule that extension ".php" is mandatory for PHP files.
Added rules for autoloading.
Added rule for one class per file.
Updated rules for comments.
Added rule for mandatory braces after "if" and "for" instructions.
Added rule for mixing PHP and HTML.
Added clarification for naming "magic methods".
Updated rule for "magic numbers".

December 2005: 
First version of ruleset described here are loosely based on guide written by Todd Hoff and Fredrik Kristiansen 
published on 2001 at http://alltasks.net/code/php_coding_standard.html (which was widely known at time PHP 
become popular language) and slightly improved with personal recommendations by authors.


-------------------------------------------------------------------------------------------------------
