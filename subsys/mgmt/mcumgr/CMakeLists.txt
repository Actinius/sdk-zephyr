# SPDX-License-Identifier: Apache-2.0

zephyr_library()
zephyr_library_sources(smp.c)

add_subdirectory(transport)
zephyr_library_sources_ifdef(CONFIG_MCUMGR_SMP_REASSEMBLY smp_reassembly.c)

add_subdirectory(lib)
zephyr_library_link_libraries(MCUMGR)

if (CONFIG_BOOT_IMAGE_ACCESS_HOOKS)
    zephyr_include_directories(
        ${ZEPHYR_MCUBOOT_MODULE_DIR}/boot/bootutil/include
        ${ZEPHYR_MCUBOOT_MODULE_DIR}/boot/zephyr/include
    )
    zephyr_library_sources(bootutil_hooks/nrf53_hooks.c)
endif()
