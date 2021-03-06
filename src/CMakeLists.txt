add_library(carmen-utils SHARED
  geometry.c
  map_interface.c
  global.c
  carmen_stdio.c
  map_read.c
  map_write.c
  carmen3d_global.c
  #laser_interface.c
  #navigator_interface.c
  )

target_link_libraries (carmen-utils z)

# make the header public
# install it to include/hello
pods_install_headers(carmen.h
  #laser_interface.h
  #navigator_interface.h
  map.h
  geometry.h
  global.h
  carmen_stdio.h
  map_interface.h
  map_messages.h
  #localize_messages.h
  base_messages.h
  map_io.h
  laser_messages.h
  robot_messages.h
  navigator_messages.h
  carmen3d_global.h
  DESTINATION carmen_utils)

# make the library public
pods_install_libraries(carmen-utils)

set(REQUIRED_LIBS
    lcmtypes_ripl-general
)

pods_use_pkg_config_packages(carmen-utils ${REQUIRED_LIBS})

# create a pkg-config file for the library, to make it easier for other
# software to use.
pods_install_pkg_config_file(carmen-utils
    CFLAGS
    LIBS -lcarmen-utils
    REQUIRES ${REQUIRED_PACKAGES}
    VERSION 0.0.1)
