project(
  'libubox',
  'c',
  default_options: ['warning_level=1'],
  meson_version: '>=0.49.0',
)

add_project_arguments('-D_GNU_SOURCE', language: 'c')

libubox_incdir = include_directories('.')

headers = files(
  'avl-cmp.h',
  'avl.h',
  'blob.h',
  'blobmsg.h',
  'blobmsg_json.h',
  'json_script.h',
  'kvlist.h',
  'list.h',
  'md5.h',
  'runqueue.h',
  'safe_list.h',
  'ulog.h',
  'uloop.h',
  'usock.h',
  'ustream.h',
  'utils.h',
  'vlist.h',
)

subdir('include-workaround-meson/libubox')

json_dep = dependency('json-c')
lua_dep = dependency('lua-5.1', required: get_option('lua'))

libubox = library(
  'libubox',
  'avl-cmp.c',
  'avl.c',
  'base64.c',
  'blob.c',
  'blobmsg.c',
  'kvlist.c',
  'md5.c',
  'runqueue.c',
  'safe_list.c',
  'ulog.c',
  'uloop.c',
  'usock.c',
  'ustream-fd.c',
  'ustream.c',
  'utils.c',
  'vlist.c',
  name_prefix: '',
  dependencies: json_dep,
  install: true,
)

depinc = include_directories('include-workaround-meson')
libubox_dep = declare_dependency(
  include_directories: depinc,
  link_with: libubox,
)

blobmsg_json = library(
  'blobmsg_json',
  'blobmsg_json.c',
  dependencies: [libubox_dep, json_dep],
  install: true,
)

blobmsg_json_dep = declare_dependency(
  include_directories: libubox_incdir,
  link_with: blobmsg_json,
)

json_script = library(
  'json_script',
  'json_script.c',
  dependencies: [libubox_dep, json_dep],
  install: true,
)

json_script_dep = declare_dependency(
  include_directories: libubox_incdir,
  link_with: json_script,
)

jshn = executable(
  'jshn',
  'jshn.c',
  dependencies: [libubox_dep, blobmsg_json_dep, json_dep],
  install: true,
)

pkg = import('pkgconfig')
pkg.generate(libubox)

install_data(
  'sh/jshn.sh',
)

install_headers(
  headers,
  subdir: 'libubox',
)

if meson.version().version_compare('>=0.54.0')
  meson.override_dependency('libubox', libubox_dep)
endif

if get_option('examples')
  subdir('examples')
endif

if lua_dep.found()
  subdir('lua')
endif

if get_option('tests')
  subdir('tests')
endif
