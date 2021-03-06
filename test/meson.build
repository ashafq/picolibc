#
# SPDX-License-Identifier: BSD-3-Clause
#
# Copyright © 2019 Keith Packard
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
#
# 1. Redistributions of source code must retain the above copyright
#    notice, this list of conditions and the following disclaimer.
#
# 2. Redistributions in binary form must reproduce the above
#    copyright notice, this list of conditions and the following
#    disclaimer in the documentation and/or other materials provided
#    with the distribution.
#
# 3. Neither the name of the copyright holder nor the names of its
#    contributors may be used to endorse or promote products derived
#    from this software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
# LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
# FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE
# COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT,
# INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
# (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
# SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT,
# STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
# ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED
# OF THE POSSIBILITY OF SUCH DAMAGE.
#
foreach target : targets
  value = get_variable('target_' + target)

  _libs = [get_variable('lib_m' + target), get_variable('lib_c' + target)]
  if is_variable('lib_semihost' + target)
    _libs += [get_variable('lib_semihost' + target)]
  endif
  if is_variable('lib_crt' + target)
    _libs += [get_variable('lib_crt'+ target)]
  endif
  
  _c_args = value[1] + test_c_args
  _link_args = value[1] + test_link_args

  t1 = 'printf/scanf'
  if target == ''
    t1_name = t1
  else
    t1_name = join_paths(target, t1)
  endif

  test(t1 + target,
       executable(t1_name, 'printf_scanf.c',
		  c_args: _c_args,
		  link_args: _link_args,
		  link_with: _libs,
		  link_depends:  test_link_depends,
		  include_directories: inc),
       env: ['MESON_SOURCE_ROOT=' + meson.source_root()])

  t1 = 'printff/scanff'
  if target == ''
    t1_name = t1
  else
    t1_name = join_paths(target, t1)
  endif

  test(t1 + target,
       executable(t1_name, 'printf_scanf.c',
		  c_args: ['-DPICOLIBC_FLOAT_PRINTF_SCANF'] + _c_args,
		  link_args: _link_args,
		  link_with: _libs,
		  link_depends:  test_link_depends,
		  include_directories: inc),
       env: ['MESON_SOURCE_ROOT=' + meson.source_root()])

  t1 = 'printf-tests'
  if target == ''
    t1_name = t1
  else
    t1_name = join_paths(target, t1)
  endif

  test(t1 + target,
       executable(t1_name, ['printf-tests.c'],
		  c_args: _c_args,
		  link_args: _link_args,
		  link_with: _libs,
		  include_directories: inc),
       env: ['MESON_SOURCE_ROOT=' + meson.source_root()])

  t1 = 'printff-tests'
  if target == ''
    t1_name = t1
  else
    t1_name = join_paths(target, t1)
  endif

  test(t1 + target,
       executable(t1_name, ['printf-tests.c'],
		  c_args: ['-DPICOLIBC_FLOAT_PRINTF_SCANF'] + _c_args,
		  link_args: _link_args,
		  link_with: _libs,
		  include_directories: inc),
       env: ['MESON_SOURCE_ROOT=' + meson.source_root()])

  t1 = 'rand'
  if target == ''
    t1_name = t1
  else
    t1_name = join_paths(target, t1)
  endif

  test(t1 + target,
       executable(t1_name, ['rand.c'],
		  c_args: _c_args,
		  link_args: _link_args,
		  link_with: _libs,
		  link_depends:  test_link_depends,
		  include_directories: inc),
	 env: ['MESON_SOURCE_ROOT=' + meson.source_root()])

  if posix_io
    t1 = 'posix-io'
    if target == ''
      t1_name = t1
    else
      t1_name = join_paths(target, t1)
    endif

    test(t1 + target,
	 executable(t1_name, ['posix-io.c'],
		    c_args: _c_args,
		    link_args: _link_args,
		    link_with: _libs,
		    link_depends:  test_link_depends,
		    include_directories: inc),
	 env: ['MESON_SOURCE_ROOT=' + meson.source_root()])
  endif

endforeach
