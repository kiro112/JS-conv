# JS-conv


## DRY Principle


[Don't Repeat Yourself](http://en.wikipedia.org/wiki/Don%27t_repeat_yourself)

## Style Manifesto

1. Whitespace
    - Never mix space with tabs.
    - When beginning a project, before you write any code, choose between soft indents (spaces) or real tabs, consider this law
        - For readability, I always recommend setting your editor's indent size to four characters &mdash; this means four spaces or four spaces representing a real tab.
    - If your editor supports it, always work with the "show invisibles" setting turned on. The benefits of this practice are:
        - Enforced consistency
        - Eliminating end of line whitespace
        - Eliminating blank line whitespace
        - Commits and diffs that are easier to read
    - Use [Editorconfig](http://editorconfig.org/) when possible.  It supports most IDEs and handles most whitespace settings.

2. Beautiful Syntax

    A. Parenthesis, Braces and Linebreaks
    ```javascript
    /*
        if/else/for/while/try always have spaces, braces and span multiple lines
        this encourage readability
        use whitespaces to promote  readability
    */

    // Bad
    if(condition) doSomething();

    // Good
    if (codintion) {
        doSomething();
    }
    

    // Bad
    while(condition) iterating++;
     
    // Good
    while (codition) {
        iterating++;
    }
    ```

    ```javascript
    /*
        Insert spaces between reserved words and (), {} and operators
    */

    // Bad
    for(var i=0;i<100;i++) someIteratingFn();

    // Good
    for (let i = 0; i < 100; i++) {
        // statement
    }
    ```

    ```javascript
    /*
        If the code block contains a lot of statements, apply proper linebreaks
    */

    // Bad
    if (condition) {
        let a = my_object.something();
        let b = confing.something();
        if (condition2) {
            let c = moreThingsTodo();
        }
    }

    // Good
    if (condition) {
        let a = my_object.something();
        let b = confing.something();
        
        if (condition2) {
            let c = moreThingsTodo();
        }
    }
    
    ```