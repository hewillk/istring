## Biomodern.Istring
`Biomodern.Istring` is just type alias to the [`basic_string<int8_t>`][basic_string], which can be using for representing the encoded string of nucleotide sequence which `0-3` indicate `ACGT`, and `4` indicates the unknown base `N`.
The head only [istring.hpp][istring_hpp] contains several utility functions for the nucleotide sequence such as:
```cpp
istring operator ""_is(const char*, size_t); // user-defined literals for the istring
size_t Codec::hash(istring); // integer encoding for istring
istring Codec::rhash(size_t, size_t); // map integer back to the istring
string Codec::rev_comp(string_view);
istring Codec::rev_comp(istring_view); // get reverse complement for the std::string/istring
```

## Compilers
- GCC 10.2

## Usage
```cpp
#include <cassert>
#include <iostream>
#include "istring.hpp"

int main() {
  using namespace std::string_literals;
  using namespace biomodern::utility;
  
  const auto s = "12031"_is;
  assert(Codec::hash(s) == 0b01'10'00'11'01);
  assert(Codec::rhash(0b01'10'00'11'01, 5) == s);
  assert(Codec::to_istring("ACNGGTT") == "0142233"_is);
  assert(Codec::rev_comp("ACNGGTT") == "AACCNGT"s);
  assert(Codec::rev_comp(s) == "20312"_is);
  std::cout << s << "\n";
}
```

[basic_string]: https://en.cppreference.com/w/cpp/string/basic_string
[istring_hpp]: https://github.com/hewillk/Biomodern.Istring/blob/main/istring.hpp
