~~~js
/** Used to generate unique IDs. */
const idCounter = {}

/**
 * Generates a unique ID. If `prefix` is given, the ID is appended to it.
 *
 * @since 0.1.0
 * @category Util
 * @param {string} [prefix=''] The value to prefix the ID with.
 * @returns {string} Returns the unique ID.
 * @see random
 * @example
 *
 * uniqueId('contact_')
 * // => 'contact_104'
 *
 * uniqueId()
 * // => '105'
 */
function uniqueId(prefix='$lodash$') {
  if (!idCounter[prefix]) {
    idCounter[prefix] = 0
  }

  const id =++idCounter[prefix]
  if (prefix === '$lodash$') {
    return `${id}`
  }

  return `${prefix + id}`
}

export default uniqueId
~~~

#源码分析：
idCounter是一个用来记录(context, counter)全局的object。
~~~js
uniqueId('contact_')
uniqueId()
console.log(idCounter) // {'contact_': 1, '$lodash$': 1}
~~~

每次用户调用`uniqueId`函数都会把与prefix相对应的counter加一。