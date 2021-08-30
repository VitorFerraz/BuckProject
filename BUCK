load("//Config:configs.bzl", "app_binary_configs", "library_configs", "watch_binary_configs", "message_binary_configs", "pretty", "info_plist_substitutions", "bundle_identifier", "DEVELOPMENT_LANGUAGE")
load("//Config:buck_rule_macros.bzl", "apple_lib", "apple_test_lib", "apple_test_all")
load("//Config:buck_local.bzl", "buck_local_apple_asset_catalog", "buck_local_binary", "buck_local_bundle",
     "buck_local_workspace")

buck_local_workspace(
    name = "workspace",
    workspace_name = "BuckProject",
    src_target = ":BuckProject",
    ui_test_target = ":XCUITests",
    native_xcode_scheme_actions={
        "Build": {
            "PRE_SCHEME_ACTIONS": ["echo 'Started'"],
            "POST_SCHEME_ACTIONS": ["echo 'Finished'"],
        },
    },
    action_config_names = {"profile": "Profile"},
)

buck_local_bundle(
    name = "BuckProject",
    visibility = [
        "//:",
    ],
    extension = "app",
    binary = ":BuckProjectBinary",
    product_name = "BuckProject",
    info_plist = "BuckProject/Info.plist",
    native_xcode_deps=[],
    buck_local_deps=[],
    info_plist_substitutions = {
        "DEVELOPMENT_LANGUAGE": DEVELOPMENT_LANGUAGE,
        "PRODUCT_BUNDLE_IDENTIFIER": bundle_identifier("BuckProject"),
        "PRODUCT_BUNDLE_PACKAGE_TYPE": "XPC!",
        "PRODUCT_MODULE_NAME": "BuckProjectBinary",
    },   
)


apple_package(
    name = "BuckProjectPackage",
    bundle = ":BuckProject",
)

apple_resource(
    name = "BuckProjectResources",
    dirs = [],
    files = glob(['BuckProject/*.png','BuckProject/*.xib','BuckProject/*.storyboard']),
)

# BuckProjectBinary
buck_local_binary(
    name = "BuckProjectBinary",
    visibility = [
        "//:",
        "//...",
    ],
    configs = app_binary_configs("BuckProject"),
    swift_version = "5",
    srcs = glob([
        "BuckProject/**/*.swift"
    ]),
    # native_xcode_deps = [":ExampleAppLibrary"],
    buck_local_deps=[
        "//BuckLocal:BuckLocal",
        "//BuckLocal:RemapDBGSourcePath",
    ],
)

apple_binary(
    name = "BuckProjectAppBinary",
    swift_version = "5",
    srcs = glob([
        "BuckProject/**/*.swift"
    ]),
    headers = glob([
        'BuckProject/**/*.h',
    ]),
    frameworks = [
        '$SDKROOT/System/Library/Frameworks/Foundation.framework',
        '$SDKROOT/System/Library/Frameworks/UIKit.framework'
    ],
)

#apple_library usado para frameworks

apple_bundle(
    name = "BuckProjectApp",
    binary = ":BuckProjectAppBinary",
    extension = "app",
    info_plist = "BuckProject/Info.plist",
    info_plist_substitutions = {
        "DEVELOPMENT_LANGUAGE": DEVELOPMENT_LANGUAGE,
        "PRODUCT_BUNDLE_IDENTIFIER": bundle_identifier("BuckProject"),
        "PRODUCT_BUNDLE_PACKAGE_TYPE": "XPC!",
        "PRODUCT_MODULE_NAME": "BuckProjectBinary",
    }
)