## Download
* https://github.com/marceljanerfont/utfcpp/tree/v3-2-1-custom/source
* branch: v3-2-1-custom

## Parent repository
* https://github.com/nemtrif/utfcpp


## v3-2-1-custom
There are only those changes in 'utf8.h':

```cpp
// standard string conversions usign utf8
#include <string>
#include <vector>

namespace utf8 {
/**
 * \brief Converts std::wstring encoded in UTF-16 if WINDOWS or UTF-32 if POSIX into a std::string encoded in UTF-8
 * \param std::wstring utf16_str encoded in UTF-16 if WINDOWS or UTF-32 if POSIX
 * \return std::string utf8_str encoded in UTF-8
 */
std::string toUtf8(const std::wstring &utf16_str) {
  std::string utf8_str;
#ifdef __linux__
  utf8::utf32to8(utf16_str.begin(), utf16_str.end(), back_inserter(utf8_str));
#else
  utf8::utf16to8(utf16_str.begin(), utf16_str.end(), back_inserter(utf8_str));
#endif
  return utf8_str;
}
/**
* \brief Converts std::string encoded in UTF-8 into std::wstring encoded in UTF-16 if WINDOWS or in UTF-32 if POSIX
* \param std::string utf8_str encoded in UTF-8
* \return std::wstring utf16_str encoded in UTF-16 if WINDOWS or UTF-32 if POSIX
*/
std::wstring fromUtf8(const std::string &utf8_str) {
  std::wstring utf16_str;
#ifdef __linux__
  utf8::utf8to32(utf8_str.begin(), utf8_str.end(), back_inserter(utf16_str));
#else
  utf8::utf8to16(utf8_str.begin(), utf8_str.end(), back_inserter(utf16_str));
#endif
  return utf16_str;
}
}
```
