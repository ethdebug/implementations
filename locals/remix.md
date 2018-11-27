## this document shortly describes how Remix debugger resolve locals

in pseudo code: ([original code](https://github.com/ethereum/remix/blob/master/remix-debug/src/solidity-decoder/internalCallTree.js#L115))
```
function buildTree (scopeId) {
  foreach (steps) {
    var source = getSourceLocation
    if (call || create || callcode || delegatecall || source.jump == 'i') { // source.jump == 'i' means jump to high level function
      buildTree(subScopeId)
    } else if (returnFromAPreviousScope) {
      // update the last step of current scope
    } else {
      // handle locals, see resolveLocals() 
    }
  }
}

function resolveLocals(step, scopeId, sourcelocation, scopes) {
 var variableDeclaration = getVariableDeclaration(sourcelocation)
 if (variableDeclaration && notAlreadySeen) {
  scopes[scopeId].locals[variableDeclaration.name] = { name, stackDepth, type, sourceLocation }
 }
 var fnDefinition = getFunctionDefinition(sourcelocation)
 if (fnDefinition && justSteppedIn) {
  foreach (params) {
    scopes[scopeId].locals[param.name] = { name, stackDepth, type, sourceLocation }
  }
 }
}
```
