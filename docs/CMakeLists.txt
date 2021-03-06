# The MIT License (MIT)
#
# Copyright (c) 2018 Mateusz Pusz
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

cmake_minimum_required(VERSION 3.2)

option(UNITS_BUILD_DOCS "Generate project documentation" ON)
if(NOT UNITS_BUILD_DOCS)
    return()
endif()

# Find all the public headers
file(GLOB_RECURSE unitsPublicHeaders "${PROJECT_SOURCE_DIR}/src/*.h")

# Sphinx documentation dependencies
set(unitsSphinxDocs
    "${CMAKE_CURRENT_SOURCE_DIR}/_static/css/custom.css"
    "${CMAKE_CURRENT_SOURCE_DIR}/_static/img/concepts.png"
    "${CMAKE_CURRENT_SOURCE_DIR}/_static/img/downcast_1.png"
    "${CMAKE_CURRENT_SOURCE_DIR}/_static/img/downcast_2.png"
    "${CMAKE_CURRENT_SOURCE_DIR}/_static/img/units.png"

    "${CMAKE_CURRENT_SOURCE_DIR}/CHANGELOG.md"

    "${CMAKE_CURRENT_SOURCE_DIR}/design.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/design/directories.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/design/downcasting.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/design/quantity.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/examples.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/avg_speed.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/box_example.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/capacitor_time_curve.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/clcpp_response.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/conversion_factor.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/custom_systems.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/foot_pound_second.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/glide_computer.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/hello_units.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/kalman_filter-alpha_beta_filter_example2.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/linear_algebra.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/measurement.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/total_energy.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/examples/unknown_dimension.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/faq.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/framework.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/framework/basic_concepts.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/framework/constants.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/framework/conversions_and_casting.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/framework/dimensions.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/framework/quantities.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/framework/quantity_points.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/framework/text_output.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/framework/units.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/genindex.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/glossary.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/index.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/introduction.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/quick_start.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/concepts.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/customization_points.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/downcasting.rst"
#   "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/functions.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/metafunctions.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types/dimensions.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types/prefixes.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types/quantity.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types/quantity_point.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types/representation.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types/units.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types/utilities.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types/utilities/basic_fixed_string.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types/utilities/basic_symbol_text.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/core/types/utilities/ratio.rst"

#   "${CMAKE_CURRENT_SOURCE_DIR}/reference/math.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/random.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/data.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/data/bitrate.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/data/information.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/data/prefixes.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/generic.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/generic/angle.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/generic/dimensionless.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/generic/unknown.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/natural.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/natural/constants.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/natural/dimensions.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/natural/units.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si_cgs.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/length.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/acceleration.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/area.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/energy.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/force.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/length.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/mass.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/power.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/pressure.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/speed.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/cgs/time.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/dimensions_and_concepts.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si_fps.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/length.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/acceleration.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/area.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/density.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/energy.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/force.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/length.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/mass.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/power.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/pressure.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/speed.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/time.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/fps/volume.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si_iau.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/iau/length.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si_imperial.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/imperial/length.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si_international.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/international/area.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/international/length.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/international/speed.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/international/volume.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/absorbed_dose.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/acceleration.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/amount_of_substance.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/area.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/capacitance.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/catalytic_activity.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/charge_density.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/concentration.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/conductance.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/constants.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/current_density.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/density.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/dynamic_viscosity.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/electric_charge.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/electric_current.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/electric_field_strength.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/energy.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/force.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/frequency.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/heat_capacity.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/inductance.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/length.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/luminance.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/luminous_intensity.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/magnetic_flux.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/magnetic_induction.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/mass.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/molar_energy.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/momentum.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/permeability.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/permittivity.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/power.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/prefixes.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/pressure.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/resistance.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/speed.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/surface_tension.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/thermal_conductivity.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/thermodynamic_temperature.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/time.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/voltage.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/volume.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si_typographic.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/typographic/length.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si_us.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/reference/systems/physical/si/us/length.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/references.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/use_cases.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/use_cases/custom_representation_types.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/use_cases/extensions.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/use_cases/legacy_interfaces.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/use_cases/linear_algebra.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/use_cases/natural_units.rst"
    "${CMAKE_CURRENT_SOURCE_DIR}/use_cases/unknown_dimensions.rst"

    "${CMAKE_CURRENT_SOURCE_DIR}/usage.rst"
)

include(documentation)
include(GNUInstallDirs)

add_documentation(documentation ALL
    BREATHE_PROJECT mp-units
    CODE_SOURCE_DIR "${PROJECT_SOURCE_DIR}/src"
    INSTALL_DIR ${CMAKE_INSTALL_DOCDIR}
    CODE_DEPENDS ${unitsPublicHeaders}
    DOCS_DEPENDS ${unitsSphinxDocs}
)
