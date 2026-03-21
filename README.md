package com.civicaid.service;

import com.civicaid.entity.AuditLog;
import org.springframework.data.domain.Page;
import org.springframework.data.domain.Pageable;

import java.time.LocalDateTime;
import java.util.List;

public interface AuditLogService {
    void log(Long userId, String action, String resource, String details, String ipAddress);
    Page<AuditLog> getAllLogs(Pageable pageable);
    Page<AuditLog> getLogsByUser(Long userId, Pageable pageable);
    Page<AuditLog> getLogsByResource(String resource, Pageable pageable);
    List<AuditLog> getLogsByDateRange(LocalDateTime from, LocalDateTime to);
}
