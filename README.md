# Coding Standards


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
    if(condition){ doSomething(); }

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
        let name;
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
        let name;

        if (condition2) {
            let c = moreThingsTodo();
        }
    }
    
    ```

    B. Assignments, Declarations, Functions ( Named, Expression, Constructor )
    
    ```javascript
    /*
        Always use const or let to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that.
    */
    
    // Bad
    superPower = new SuperPower();

    // Good
    const superPower = new SuperPower();
    ```

    Use one const/let per variable
    > Why? It’s easier to add new variable declarations this way, and you never have to worry about swapping out a ; for a , or introducing punctuation-only diffs. You can also step through each declaration with the debugger, instead of jumping through all of them at once.

    ```javascript
    // not actually bad
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z',
        array = [],
        object = {};

    // will be a problem if
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';
        array = [],
        object = {};

    
    // better
    const items = getItems;
    const goSportsTeam = true;
    const dragonball = 'z';
    const array = [];
    const object = {}
    ```

    ```javascript
    /*
        Horizontal alignment: DISCOURAGED
    /*
    // permitted but future edits may leave it unaligned
    {
        tiny:   42,
        longer: 435
    }

    // prefer
    {
        tiny: 42,
        longer: 435
    }
    ```

    ```javascript
    /*
        Group all your consts and then group all your lets.
        Declare initialized variables first
        Followed by uninitialized variables
        Followed by functions
    */

    // bad
    let i, len, dragonball, 
    initValue = 0,
    items = getItems(),
    goSportsTeam = true;

    // bad
    function foo () {}
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;
    let initValue = 0;

    // good
    const goSportsTeam = true;
    const items = getItems();
    
    let initValue = 0;
    let i;
    let len;
    
    function foo () {}
    ```

    ```javascript
    /*
        Variable declaration should always the first statement
        It's like listing ingredients before you cook
    */

    // Bad
    function foo () {
        // some statement
        const a = 3;
    }

    // Good
    function foo () {
        const a = 3;

        // some statement
    }

    ```

    C. Consistency Always Win
    
    ```javascript
    if (condition) {
        // statements
    }

    while (condition) {
        // statements
    }

    for (declaration; condition; increment/decrement) {
        // statements
    }

    if (condition) {
        // statements
    }
    else {
        // statements
    }

    switch (foo) {
        case 1 :
            // statements
            break;

        case 2 :
            // statements
            break;

        case 3 :
            // statements
            break;

        default :
            // statements
    }

    const foo = [1, 2, 3];
    const bar = {
        prop1: value,
        prop2: value2
    };

    if (foo === bar) {

    }

    let foo = 1 + (1 * 2);
    ```

    D. Quotes

    ```javascript
    /*
        Use single quotes `' for strings
        template literal for string interpolation or new lines
    */

    // bad
    const foo = "Some value";

    // bad - template literals should contain interpolation or newlines
    const foo = `Some value`;

    // good
    const foo = 'Some value';
    const foo = `Some value ${variable}`;
    ```

    E. End of Lines and Empty Lines

        Whitespace can ruin diffs and make changesets impossible to read. Consider incorporating a pre-commit hook that removes end-of-line whitespace and blanks spaces on empty lines automatically.

    F. **NEVER USE eval() !**
    
    It opens too many vulnerabilities
        - Improper use of eval opens up your code for injection attacks
        - Debugging can be more challenging (no line numbers, etc.)
        - eval'd code executes slower (no opportunity to compile/cache eval'd code)


    G. Forming and Accessing objects and arrays
    ```javascript
    /*
        When forming an object, don't put quotes on the property unless needed
    */
    
    // bad
    const obj = {
        'prop1': 'foo',
        'prop2': 'bar'
    };

    // Good
    const obj = {
        prop1: 'foo',
        prop2: 'bar',
    };
    ```

    ```javascript
    /*
        Always always always access properties using dot notation unless not allowed
    */

    // Bad
    obj['prop'] = 'new_value';

    // Good
    obj.prop = 'new_value';
    obj['special-property'] = 'new_value';

    ```

    ```javascript
    /*
        When forming an array, just try to have a good alignment
    */

    // Bad
    var obj = ['something', 'something_again'];

    // Good
    var obj = [
        'something',
        'something_again'
    ];
    ```

    ```javascript
    /*
        Make the object/array a one-liner if there's only 1 property/element
        and the value is not that long
    */

    // Bad
    var obj = {
        prop1 : 'value1'
    };

    var array = [
        'something'
    ];

    // Good
    var obj = {prop1: 'value1'};

    var array = ['something'];
    ```

    H. Ternary Operators
    
    ```javascript
    // Note that if the condition and values are short, one-liner is fine. Example:
    let temp = hidden ? 10 : 5;

    // bad
    const foo = maybe1 > maybe2
        ? "bar"
        : value1 > value2 ? "baz" : null;

    // split into 2 separated ternary expressions
    const maybeNull = value1 > value2 ? 'baz' : null;

    // better
    const foo = maybe1 > maybe2
        ? 'bar'
        : maybeNull;

    /*
        Avoid unneeded ternary statements
    */
    // bad
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;

    // good
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```

    I. Control Statement

    In case your control statement (if, while etc.) gets too long or exceeds the maximum line length, each (grouped) condition could be put into a new line. The logical operator should begin the line.

    > Why? Requiring operators at the beginning of the line keeps the operators aligned and follows a pattern similar to method chaining. This also improves readability by making it easier to visually follow complex logic.

    ```javascript
    // bad
    if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
        thing1();
    }

    // bad
    if (foo === 123 &&
        bar === 'abc') {
        thing1();
    }

    // bad
    if (foo === 123
        && bar === 'abc') {
        thing1();
    }

    // bad
    if (
        foo === 123 &&
        bar === 'abc'
    ) {
        thing1();
    }

    // good
    if (
        foo === 123
        && bar === 'abc'
    ) {
        thing1();
    }

    // good
    if (
        (foo === 123 || bar === 'abc')
        && doesItLookGoodWhenItBecomesThatLong()
        && isThisReallyHappening()
    ) {
        thing1();
    }

    // good
    if (foo === 123 && bar === 'abc') {
        thing1();
    }
    ```

3. Type Checking
    
    A. Actual Types

    String:
    ```javascript
    typeof variable === "string"
    ```
    
    Number:
    ```javascript
    typeof variable === "number"
    ```

    Boolean:
    ```javascript
    typeof variable === "boolean"
    ```

    Object:
    ```javascript
    typeof variable === "object"
    ```

    Array:
    ```javascript
    Array.isArray( arrayLikeObject )
    ```

    Null:
    ```javascript
    variable === null
    ```

    Undefined:
    ```javascript
    typeof variable === 'undefined'
    ```

    null or undefined or 0 or '':
    ```javascript
    !variable
    ```

    property exists :
    ```javascript
    object.hasOwnProperty(prop)
    ```


    B. Coerced Types
    ```javascript
    // string to number
    +'1'; // 1
    // or
    parseInt('1'); // 1

    // to boolean
    !!variable;

    // to string
    '' + variable;
    // or
    variable.toString();
    ```

4. Conditional Evaluation

    ```javascript
    // When only evaluating that an array has elements/length
    // instead of this:
    if (array.length > 0) ...

    // ...evaluate truthiness, like this:
    if (array.length) ...


    // instead of this:
    if (array.length === 0) ...

    // ...evaluate truthiness, like this:
    if (!array.length) ...


    // When only evaluating that a string is not empty,
    // instead of this:
    if ( string !== "" ) ...

    // ...evaluate truthiness, like this:
    if ( string ) ...
    ```

5. Naming

    Avoid single letter names.

    ```javascript
    /*
        snake_case on variables including functions
    */
    let foo_bar;


    // Do not use trailing or leading underscores
    let _firstName;
    let _firstName___;
    ```

6. Misc

    ```javascript
    /*
        If the function has a lot of arguments,
        try adding line breaks to make it more readable
    */

    // Bad
    do_this(this_one, plus_this_one, true, [this_also, this_also2]);

    // Good
    do_this(
        this_one,
        plus_this_one,
        true,
        [this_also, this_also2]
    );
    ```

    ```javascript
    // Use built-in functions as much as possible

    // Use forEach to traverse an array
    // promotes readability
    array.forEach(function (element, index, array) {

    });

    // Use filter to filter array
    // promotes readability

    array = array.filter(function (element, index, array) {
        return element.property === bar;
    });

    // Use map to modify an array
    // promotes readability

    array = array.map(function (element, index, array) {
        element.created_at = new Date;
        delete element.foo;
        return element;
    });

    // chain forEach, filter, map if possible
    // promotes readability

    array
        .filter(function (element) {
            return element.count > 50;
        })
        .map(function (element) {
            element.count += 100;
            return element;
        })
        .forEach(function (element) {
            foo(element);
        });
    ```



<!-- 
    source:
    https://github.com/rwaldron/idiomatic.js/
    https://github.com/airbnb/javascript
    https://google.github.io/styleguide/jsguide.html#features-string-literals
    https://github.com/anyTV/JS-conventions/blob/master/README.md
    -->