#### Enable error reporting (PHP)

> error_reporting (E_ALL | E_STRICT); 

> ini_set ('display_errors', 'On');

#### Reporting levels
- E_ALL - All errors and warnings (doesn't include E_STRICT)
- E_ERROR - fatal run-time errors
- E_RECOVERABLE_ERROR - almost fatal run-time errors
- E_WARNING - run-time warnings (non-fatal errors)
- E_PARSE - compile-time parse errors
- E_NOTICE - run-time notices (these are warnings which often result
from a bug in your code, but it's possible that it was
intentional (e.g., using an uninitialized variable and
relying on the fact it's automatically initialized to an
empty string)
- E_STRICT - run-time notices, enable to have PHP suggest changes
to your code which will ensure the best interoperability
and forward compatibility of your code
- E_CORE_ERROR - fatal errors that occur during PHP's initial startup
- E_CORE_WARNING - warnings (non-fatal errors) that occur during PHP's
initial startup
- E_COMPILE_ERROR - fatal compile-time errors
- E_COMPILE_WARNING - compile-time warnings (non-fatal errors)
- E_USER_ERROR - user-generated error message
- E_USER_WARNING - user-generated warning message
- E_USER_NOTICE - user-generated notice message
