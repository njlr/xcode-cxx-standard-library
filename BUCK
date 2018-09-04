from hashlib import sha256

paths = [
  '/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/include/c++/v1', 
  '/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/lib/clang/9.1.0/include', 
  '/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/include', 
  '/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/include/pthread', 
  '/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/usr/include', 
]

def extract(path): 
  name = 'headers-' + sha256(path).hexdigest()[:16]
  genrule(
    name = name, 
    out = 'include', 
    cmd = 'cp -r ' + path + ' $OUT', 
  )
  return ':' + name

extracted = [ extract(path) for path in paths ]

prebuilt_cxx_library(
  name = 'cxx-standard-library', 
  header_namespace = '', 
  header_only = True, 
  header_dirs = extracted, 
  visibility = [
    'PUBLIC', 
  ], 
)

cxx_binary(
  name = 'hello', 
  srcs = [
    'hello.cpp', 
  ],
  deps = [
    ':cxx-standard-library', 
  ], 
)
