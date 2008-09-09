import libtbx.load_env
Import("env_base","env_etc")

env_etc.annlib_dist = libtbx.env.dist_path("annlib")
env_etc.annlib_include = [env_etc.norm_join(env_etc.annlib_dist,"src"),
                          env_etc.norm_join(env_etc.annlib_dist,"include")]
env_etc.annlib_adaptbx_dist = libtbx.env.dist_path("annlib_adaptbx")
env_etc.annlib_adaptbx_include = env_etc.norm_join(
                  env_etc.annlib_adaptbx_dist,"include")

env_etc.annlib_common_includes = [
  env_etc.libtbx_include,
  env_etc.scitbx_include,
  env_etc.boost_adaptbx_include,
  env_etc.boost_include,
  env_etc.annlib_dist,    # for the adaptor cpp files
  env_etc.annlib_include[0],
  env_etc.annlib_include[1],
  env_etc.annlib_adaptbx_include,
]

env = env_base.Copy(
  CCFLAGS=env_etc.ccflags_base,
  CXXFLAGS=env_etc.cxxflags_base,
  SHCXXFLAGS=env_etc.cxxflags_base,
  SHLINKFLAGS=env_etc.shlinkflags,
)

if (env_etc.static_libraries): builder = env.StaticLibrary
else:                          builder = env.SharedLibrary
builder(target='#lib/ann',
  source = ["../annlib/src/ANN.cpp",
            "../annlib/src/bd_fix_rad_search.cpp",
            "../annlib/src/bd_pr_search.cpp",
            "../annlib/src/bd_search.cpp",
            "../annlib/src/bd_tree.cpp",
            "../annlib/src/brute.cpp",
            "../annlib/src/kd_dump.cpp",
            "../annlib/src/kd_fix_rad_search.cpp",
            "../annlib/src/kd_pr_search.cpp",
            "../annlib/src/kd_search.cpp",
            "../annlib/src/kd_split.cpp",
            "../annlib/src/kd_tree.cpp",
            "../annlib/src/kd_util.cpp",
            "../annlib/src/perf.cpp",
            "self_include/ANN.cpp",
            "self_include/bd_fix_rad_search.cpp",
            "self_include/bd_pr_search.cpp",
            "self_include/bd_search.cpp",
            "self_include/bd_tree.cpp",
            "self_include/brute.cpp",
            "self_include/kd_dump.cpp",
            "self_include/kd_fix_rad_search.cpp",
            "self_include/kd_pr_search.cpp",
            "self_include/kd_search.cpp",
            "self_include/kd_split.cpp",
            "self_include/kd_tree.cpp",
            "self_include/kd_util.cpp",
            "self_include/perf.cpp",
            "ann/ann_adaptor.cpp"
           ],
  CPPPATH=env_etc.annlib_common_includes )

if (not env_etc.no_boost_python):
  Import("env_no_includes_boost_python_ext")

  env_annlib_boost_python_ext = env_no_includes_boost_python_ext.Copy()

  env_etc.include_registry.append(
    env=env_annlib_boost_python_ext,
    paths=env_etc.annlib_common_includes + [env_etc.python_include])

  Export("env_annlib_boost_python_ext")

  SConscript("ann/boost_python/SConscript")
