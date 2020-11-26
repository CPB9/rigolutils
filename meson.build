project('rigolutils', ['c', 'cpp'], default_options : ['c_std=c99'])


libusb_dep = dependency('libusb-1.0')
if not libusb_dep.found()
    message('Using bundled libusb')
    libusb = subproject('libusb')
    libusb_dep = libusb.get_variable('libusb_dep')
endif

src = [
	'src/freetmc_local.cpp',
]

inc = include_directories('.', 'src')

cc = meson.get_compiler('cpp')
args = ['-w']
enc_arg = '-Wno-error=invalid-source-encoding'
if cc.has_argument(enc_arg)
  args += enc_arg
endif

rigolutils_lib = static_library('librigolutils',
  sources : src,
  name_prefix: 'lib',
  include_directories : inc,
  cpp_args : args,
  dependencies: [libusb_dep]
)

rigolutils_dep = declare_dependency(link_with: rigolutils_lib,
  include_directories: inc,
)
