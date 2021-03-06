##A full-scale PHP 5.3.2+ sandbox class that utilizes [PHP-Parser](https://github.com/nikic/PHP-Parser) to prevent sandboxed code from running unsafe code.

It also utilizes [FunctionParser](https://github.com/jeremeamia/FunctionParser) to disassemble callables passed to the sandbox, so that PHP callables can also be run in sandboxes without first converting them into strings.

##Features:

- Finegrained whitelisting and blacklisting, with sensible defaults configured.
- Can redefine internal PHP and other functions to make them more secure for sandbox usage.
- Can redefine superglobals and magic constants to expose your own values to sandboxed code.
- Can overwrite the get_defined_* and get_declared_* functions to show only allowed functions, classes, etc. to the sandboxed code.
- Can selectively allow and disallow function creation, class declarations, constant definitions, keywords, and much more.
- Can prepend and append trusted code to setup and tear the sandbox, and automatically whitelist the classes, functions, variables, etc. they define for the sandbox.
- Can retrieve the generated sandbox code for later usage.
- Can pass arguments directly to the sandboxed code through the execute method to reveal chosen outside variables to the sandbox.
- Can access the parsed, prepared and generated code ASTs for further analysis or for serialization.

##Example usage:

    function test($string){
        return 'Hello ' . $string;
    }

    $sandbox = new PHPSandbox\PHPSandbox;
    $sandbox->whitelist_func('test');
    $result = $sandbox->execute(function(){
        return test('world');
    });

    var_dump($result);  //Hello world

##Requirements

- PHP 5.3.2+
- PHP-Parser
- FunctionParser (if you wish to use closures)
- PHP should be compiled with --enable-tokenizer option (it typically is)

##LICENSE

    Copyright (c) 2013 by Elijah Horton (fieryprophet [at] yahoo.com)

    Some rights reserved.

    Redistribution and use in source and binary forms, with or without
    modification, are permitted provided that the following conditions are
    met:

        * Redistributions of source code must retain the above copyright
          notice, this list of conditions and the following disclaimer.

        * Redistributions in binary form must reproduce the above
          copyright notice, this list of conditions and the following
          disclaimer in the documentation and/or other materials provided
          with the distribution.

        * The names of the contributors may not be used to endorse or
          promote products derived from this software without specific
          prior written permission.

    THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
    "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
    LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
    A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
    OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
    SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
    LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
    DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
    THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
    (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
    OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.