private void autoCompleteProgamIfAllSchemesInactive(Long programId) {
        Program program = programRepository.findById(programId).orElse(null);
        if (program == null || program.getStatus() != Program.ProgramStatus.ACTIVE) return;
 
        List<Scheme> schemes = schemeRepository.findByProgram_ProgramId(programId);
        boolean allInactive = !schemes.isEmpty()
                && schemes.stream().allMatch(s -> s.getStatus() == Scheme.SchemeStatus.INACTIVE);
 
        if (allInactive) {
            program.setStatus(Program.ProgramStatus.COMPLETED);
            programRepository.save(program);
        }
    }
